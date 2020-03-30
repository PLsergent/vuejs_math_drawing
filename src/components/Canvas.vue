<template>
  <div id="VueCanvas"></div>
</template>

<script>
import JXG from "jsxgraph";

export default {
  props: {
    formulas: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      curves: []
    };
  },
  name: "VueCanvas",
  methods: {
    f(data) {
      // eslint-disable-next-line
      const x = data;
      try {
        const res = eval(this.formula);
        return res;
      } catch (e) {
        if (e instanceof SyntaxError) {
          return null;
        }
      }
      return eval(this.formula);
    }
  },
  watch: {
    formulas: function(data) {
      this.board.removeObject(this.curves);
      this.curves = [];
      if (data.length === 0) return;
      data.forEach(formula => {
        this.formula = formula;
        this.curves.push(
          this.board.create("functiongraph", [this.f /* minx,maxx*/])
        );
      });
    }
  },
  mounted() {
<<<<<<< HEAD
    this.board = JXG.JSXGraph.initBoard("VueCanvas", {
      boundingbox: [-1, 1, 1, -1],
      axis: true
=======
    var board = JXG.JSXGraph.initBoard('vue-canvas', { 
      boundingbox: [-1, 5, 1, -5], axis:true
      // x1 y1 x2 y2
>>>>>>> 5ffd5b842108b42ae4bb52610662e2e2630f4e17
    });

    var elt = document.getElementById("VueCanvas_licenseText");
    elt.style.display = "none";

<<<<<<< HEAD
    // var p = board.create('point', [1,1], {style:6, name:'p'});
=======
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
>>>>>>> 5ffd5b842108b42ae4bb52610662e2e2630f4e17
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
<<<<<<< HEAD
#VueCanvas {
  display: block;
  margin: 0 auto;
=======
#vue-canvas {
  display: flex;
  justify-content: center;
  align-self: center;
>>>>>>> 5ffd5b842108b42ae4bb52610662e2e2630f4e17
  padding: 0;
  width: 100%;
  height: 80vh;
  overflow: hidden;
}
</style>
