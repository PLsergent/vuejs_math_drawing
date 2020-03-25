<template>
  <div id="vue-canvas"></div>
</template>

<script>
import JXG from "jsxgraph";

export default {
  name: "VueCanvas",
  mounted() {
    var board = JXG.JSXGraph.initBoard('vue-canvas', { 
      boundingbox: [-5, 5, 5, -5], axis:true
    });

    var elt = document.getElementById("vue-canvas_licenseText");
    elt.style.display = "none";

    // Macro function plotter
    function addCurve(board, func, atts) {
        var f = board.create('functiongraph', [func], atts);
        return f;
    }
    
    // Simplified plotting of function
    function plot(func, atts) {
      if (atts==null) {
          return addCurve(board, func, {strokewidth:2});
      } else {
          return addCurve(board, func, atts);
      }    
    }

    var p = board.create('point', [1,1], {style:6, name:'p'}); 

    function f(x) {
      return Math.cos(x)*p.Y();
    }

    plot(f);
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
