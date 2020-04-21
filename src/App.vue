<template>
  <div id="app">
    <form>
      <section>
        <h2>Math drawing</h2>
        <p>Boundings on x :</p>
        <input type="number" step="0.1" value="-1.5" max="-0.5" v-model="bounds[0]" />
        <input type="number" step="0.1" value="1.5" min="0.5" v-model="bounds[1]" />
        <hr>
        <button v-on:click="addFormulaInput($event)">Add formula</button>
        <div v-for="(formula, index) in formulas" :key="index">
          <input type="checkbox" v-model="visible[index]" />
          <input
            type="text"
            :disabled="visible[index]"
            v-model="formulas[index]"
            class="form-control form-control-lg"
            v-on:keydown.enter.prevent
          />
          <input type="color" v-model="colors[index]" />
          <button v-on:click="removeFormulaInput($event,index)">-</button>
        </div>
      </section>
    </form>
  
    <VueCanvas :formulas="visibleFormulas" :boundings="boundings" />
  
  </div>
</template>

<script>
import VueCanvas from "./components/Canvas.vue";

export default {
  name: "App",
  components: {
    VueCanvas
  },
  data() {
    return {
      formulas: [""],
      visible: [false],
      colors: ["#000000"],
      bounds: [-1.5, 1.5]
    };
  },
  computed: {
    visibleFormulas() {
      const res = [];
      for (const [index, formula] of this.formulas.entries()) {
        if (this.visible[index]) {
          var push = [formula, this.colors[index]];
          res.push(push);
        }
      }
      return res;
    },
    boundings() {
      return this.bounds;
    }
  },
  methods: {
    addFormulaInput(e) {
      this.visible.push(false);
      this.formulas.push("");
      this.colors.push("#000000")
      e.preventDefault();
    },
    removeFormulaInput(e, index) {
      if (this.formulas.length > 1) {
        this.visible.splice(index, 1);
        this.formulas.splice(index, 1);
        this.colors.splice(index, 1);
      }
      e.preventDefault();
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
