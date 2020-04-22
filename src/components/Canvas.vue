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
  computed: {
    watchout() {
      return this.formulas, this.boundings;
      // so we can call a single watcher for two props
    }
  },
  watch: {
    watchout() {
      var data = this.formulas;
      var bounds = this.boundings;

      // remove all furves
      this.board.removeObject(this.curves);
      this.curves = [];

      // return if null
      if (data.length === 0) return;

      // update the boundings
      this.board.setBoundingBox([bounds[0], 1.5, bounds[1], -1.5]);
      // for each tuple [f(x), color]
      data.forEach(tuple => {
        this.formula = tuple[0];
        this.color = tuple[1];
        this.curves.push(
          this.board.create("functiongraph", [this.f, bounds[0], bounds[1]], { strokeColor: this.color, strokeWidth: 1.25 })
        )
      });
    }
  },
  mounted() {
    this.board = JXG.JSXGraph.initBoard("VueCanvas", {
      boundingbox: [-1.5, 1.5, 1.5, -1.5],
      // -x, y, x, -y
      axis: true
    });

    // Remove elements from the canva
    var elt = document.getElementById("VueCanvas_licenseText");
    var elt1 = document.getElementById("VueCanvas_navigationbar");
    elt.style.display = "none";
    elt1.style.display = "none";
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
