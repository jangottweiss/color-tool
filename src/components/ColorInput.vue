<template>
  <div class="component">  
    <el-row :gutter="20" type="flex" justify="space-around">
      <el-col :span="20"><div>
         <el-input    
            size="large"            
            v-model="colorInput">
        </el-input>  
        <el-color-picker v-model="colorInputPicker" @change="colorPickerChange"></el-color-picker>    
      </div>
    </el-col>
    </el-row>
                 
  </div>
</template>

<script>
import chroma from "chroma-js";
export default {
  name: "ColorInput",
  props: ['startColor'],
  created: function () {    
    this.colorObject = chroma(this.startColor);
    this.colorInputPicker = this.colorObject.hex();
    this.colorInput = this.colorObject.hex();
  },
  data() {
    return {
      colorInput: "#D4F880",
      colorObject: chroma("#D4F880"),
      colorInputPicker: "#D4F880"
    };
  },
  methods: {
    newColor(c) {
      this.$emit("newColor", c);
    },
    colorPickerChange() {    
      this.colorObject = chroma(this.colorInputPicker); 
      this.colorInput = this.colorObject.hex();
      this.newColor(this.colorObject);
    }
  },
  watch: {   
    colorInput: function(newColorInput) {
      let color;
      try {
        this.colorObject = chroma(newColorInput);        
        this.newColor(this.colorObject);
        this.colorInputPicker = this.colorObject.hex();
      } catch (error) {
        console.log(error);
        return;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
</style>
