<template>
  <div id="container" v-bind:style="{ backgroundColor: bgColor}">   
    <div id="app">
      <ColorInput @newColor="newColor" v-bind:startColor="bgColor" />
    </div>
    
  </div>
</template>

<script>
import chroma from "chroma-js";
import ColorInput from './components/ColorInput.vue'

const startColor = "#D4F880";

export default {
  name: 'app',
  components: {
    ColorInput
  },
  data() {
    return {
      bgColor: startColor,
      color: chroma(startColor)
    }
  },
  methods: {
    newColor(c) {
      this.bgColor = c.hex();
    }
  }
}
</script>

<style>
body {
  margin: 0px;
  padding: 0px;
}

#container {
  width: 100;
  height: 100%;
  position: absolute;
  top: 0; bottom: 0px; left: 0px; right: 0px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#app {
  margin: 50px;
}
</style>
