<template>
<v-app>
<div class="main-content" style="display:flex; justify-content:center">
  
  <div v-for="light in lights" :key="light.id">
    {{ light.name }}

    <v-color-picker mode="rgba" v-model="light.val" @input="event => debouncedChangeColour(light.id, event)"></v-color-picker>
  </div>

</div>
</v-app>

</template>

<script>
// import { changeColour as utilChangeColour } from '~/utils/lights';
import { debounce, throttle } from 'lodash'
export default {
  data() {
    return {
      lights: [
        { name: "Strip", id: "bfb2e8e952b6596d6d9180", val: { r: 255, g: 1, b: 1 } },
      ]
    }
  },
  methods: {
    changeColour(id, event) {
      const {r,g,b} = event
      console.log(r,g,b)
      this.$axios.get(`http://192.168.0.35/${r},${g},${b}`)
    },
    debouncedChangeColour() {}
  },
  mounted() {
    this.debouncedChangeColour = throttle(this.changeColour, 50, {
      leading: true,
      trailing: true
    })
  }
}
</script>

<style>

</style>