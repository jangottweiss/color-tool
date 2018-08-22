<template>
  <div class="content" v-bind:style="{ backgroundColor: bgColor}">
    <header>
    </header>
    <section class="center">
      <ColorInput @newColor="newColor" v-bind:startColor="bgColor" />  
    </section>
    <footer class="footer" v-bind:style="{ backgroundColor: color.hex()}">
      <ColorShades v-bind:color="color" />
    </footer>  
  </div>      
</template>

<script>
import chroma from "chroma-js";
import ColorInput from "./components/ColorInput.vue";
import ColorShades from "./components/ColorShades.vue";

const startColor = chroma.random();

export default {
  name: "app",
  components: {
    ColorInput,
    ColorShades
  },
  data() {
    return {
      bgColor: startColor,
      color: startColor
    };
  },
  methods: {
    newColor(c) {
      this.bgColor = c.hex();
      this.color = c;
    }
  }
};
</script>

<style>
html,
body {
  height: 100%;
  margin: 0;
}
html > body .content {
  height: auto;
}
.content {
  height:100%;
  min-height:100%;/*for mozilla*/
}

.footer {
  background-color: aliceblue;
  position: absolute;
  bottom: 0px;
  height: 250px;
  width: 100%
}

.center {
  width: 50%;
  height: 250px;

  position: absolute; /*it can be fixed too*/
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;

  /*this to solve "the content will not be cut when the window is smaller than the content": */
  max-width: 100%;
  max-height: 100%;
  overflow: auto;
}
</style>
