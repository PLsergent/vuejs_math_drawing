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
    },

    boundings: {
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
      const x = data; // to compute values of x
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
    formulas: function() {
      var data = this.formulas;
      this.board.removeObject(this.curves);
      this.curves = [];
      if (data.length === 0) return;
      this.board.setBoundingBox([this.boundings[0], 1.5, this.boundings[1], -1.5]);
      data.forEach(tuple => {
        this.formula = tuple[0];
        this.color = tuple[1];
        this.board.create("functiongraph", [this.f, this.boundings[0], this.boundings[1]], { strokeColor: this.color, strokeWidth: 1.25 })
      });
    }
  },
  mounted() {
    this.board = JXG.JSXGraph.initBoard("VueCanvas", {
      boundingbox: [-1.5, 1.5, 1.5, -1.5],
      // -x, y, x, -y
      axis: true
    });

    var elt = document.getElementById("VueCanvas_licenseText");
    elt.style.display = "none";
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#VueCanvas {
  display: block;
  margin: 0 auto;
  padding: 0;
  width: 100%;
  height: 70vh;
  overflow: hidden;
}
</style>
