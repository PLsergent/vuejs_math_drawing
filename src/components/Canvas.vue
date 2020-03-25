<template>
  <div id="vue-canvas"></div>
</template>

<script>
import JXG from "jsxgraph";

export default {
  name: "VueCanvas",
  mounted() {
    JXG.JSXGraph.initBoard("vue-canvas", {
      boundingbox: [-5, 5, 5, -5],
      axis: true
    });
    var elt = document.getElementById("vue-canvas_licenseText");
    elt.style.display = "none";
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#vue-canvas {
  display: block;
  margin: 0 auto;
  padding: 0;
  width: 1000px;
  height: 500px;
  border-radius: 20px;
  overflow: hidden;
}
</style>
