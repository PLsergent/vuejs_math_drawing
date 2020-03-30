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
    this.board = JXG.JSXGraph.initBoard("VueCanvas", {
      boundingbox: [-1, 1, 1, -1],
      axis: true
    });

    var elt = document.getElementById("VueCanvas_licenseText");
    elt.style.display = "none";

    // var p = board.create('point', [1,1], {style:6, name:'p'});
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#VueCanvas {
  display: block;
  margin: 0 auto;
  padding: 0;
  width: 1000px;
  height: 500px;
  border-radius: 20px;
  overflow: hidden;
}
</style>
