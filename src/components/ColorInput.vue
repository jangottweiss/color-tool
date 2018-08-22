<template>
  <div class="component">  
      <el-card class="box-card">
    <el-row :gutter="20" justify="space-around" type="flex">
        <el-col :span="20">
            <div class="grid-content bg-purple">
                <el-input maxlength="7" size="large" pattern="[a-fA-F\d]+" v-model="inputHEX">
                     <template slot="prepend">#</template>    
                </el-input> 
            </div>
        </el-col>
    </el-row>

    <el-row :gutter="20" justify="space-around" type="flex">
        <el-col :span="20">
            <div class="grid-content bg-purple">
                <el-input size="large" v-model="inputRGB">
                     <template slot="prepend">rgb</template>    
                </el-input> 
            </div>
        </el-col>
    </el-row>

    <el-row :gutter="20" justify="space-around" type="flex">
        <el-col :span="20">
            <div class="grid-content bg-purple">
                <el-color-picker v-model="inputPicker" @change="colorPickerChange"></el-color-picker>    
            </div>
        </el-col>
    </el-row>
      </el-card>
  </div>
</template>

<script>
import chroma from "chroma-js";
export default {
  name: "ColorInput",
  props: ["startColor"],
  created: function() {
		this.colorObject = chroma(this.startColor);
		this.inputHEX = this.colorObject.hex();
	},
  data() {
    return {
      colorObject: "",
      inputHEX: "",
      inputRGB: "",
      inputPicker: ""
    };
  },
  methods: {
    newInput(input) {
      try {
				this.colorObject = chroma(input);
				this.newColor(this.colorObject);
      } catch (error) {
        console.log(error);
        return;
      }
    },
    newColor(c) {
      this.$emit("newColor", c);
    },
		colorPickerChange() {
			this.newInput(this.inputPicker);
			this.inputHEX = this.colorObject.hex();
		},
		test() {
			console.log("TEST")
		}
		
  },
  watch: {
    inputHEX: function(newColorInput) {
      if (newColorInput.length < 6) return;
			this.newInput(newColorInput);
			this.inputRGB = this.colorObject.rgb();
      this.inputPicker = this.colorObject.hex();
    },
    inputRGB: function(newColorInput) {
      if (newColorInput.length < 3) return;
      this.newInput(newColorInput.split(","));
      this.inputHEX = this.colorObject.hex();
      this.inputPicker = this.colorObject.hex();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.el-row {
  margin-bottom: 20px;
}
</style>
