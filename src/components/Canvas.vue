<template>
  <div id="vue-canvas"></div>
</template>

<script>
import JXG from "jsxgraph";

export default {
  name: "VueCanvas",
  mounted() {
    var board = JXG.JSXGraph.initBoard('vue-canvas', { 
      boundingbox: [-1, 5, 1, -5], axis:true
      // x1 y1 x2 y2
    });

    var elt = document.getElementById("vue-canvas_licenseText");
    elt.style.display = "none";

    function f(x) {
      return 2*Math.cos(3*x) - Math.sin(x);
    }

    plot(f);
    
    // Simplified plotting of function
    function plot(func, atts) {
      if (atts==null) {
          return addCurve(board, func, {strokewidth:2});
      } else {
          return addCurve(board, func, atts);
      }    
    }

    // Macro function plotter
    function addCurve(board, func, atts) {
        var f = board.create('functiongraph', [func], atts);
        return f;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#vue-canvas {
  display: flex;
  justify-content: center;
  align-self: center;
  padding: 0;
  width: 100%;
  height: 80vh;
  overflow: hidden;
}
</style>
