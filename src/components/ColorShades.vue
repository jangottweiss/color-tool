<template>
  <div class="component">  
      <el-row :gutter="20" justify="space-around" type="flex">
        <el-col :span="5" v-for="(item, index) in shadesBright" v-bind:key="index">
            <div class="swatch" v-bind:style="{ backgroundColor: item.hex()}">
                <div class="value">
                    {{item.hex()}} <br>
                    rgb({{item.rgb().join(",")}})
                </div>                
                 
            </div>
        </el-col>
    </el-row>
     <el-row :gutter="20" justify="space-around" type="flex">
         <el-col :span="5" v-for="(item, index) in shadesDark" v-bind:key="index">
            <div class="swatch" v-bind:style="{ backgroundColor: item.hex()}">                
                  <div class="value">
                    {{item.hex()}} <br>
                    rgb({{item.rgb().join(",")}})
                </div>                
            </div>
        </el-col>
    </el-row>
   
  </div>
</template>

<script>
import chroma from "chroma-js";
export default {
  name: "ColorInput",
  props: ["color"],
  created: function() {
    this.calculateShades(this.color);
  },
  data() {
    return {
      shades: [0.25, 0.5, 0.75, 1],
      shadesBright: [],
      shadesDark: []
    };
  },
  methods: {
    calculateShades(color) {
      this.shadesBright = [];
      this.shadesDark = [];
      this.shades.forEach((f, i) => {
        this.shadesBright.push(color.brighten(f));
        this.shadesDark.push(color.darken(f));
      });
    }
  },
  watch: {
    color: function(newColor) {
      this.calculateShades(newColor);
    }
  }
};
</script>

<style scoped>
.el-row {
  margin-bottom: 10px;
  margin-top: 10px;
}
.swatch {
  height: 100px;
  width: 100%;
}
.value {
  text-align: center;
  padding: 10% 0;
}
</style>
