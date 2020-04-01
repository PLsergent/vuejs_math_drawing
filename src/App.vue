<template>
  <div id="app">
    <form>
      <section>
        <h3>Entrer votre formule :</h3>

        <div v-for="(formula,index) in formulas" :key="index">
          <input type="checkbox" v-model="visible[index]" />
          <input
            type="text"
            :disabled="visible[index]"
            v-model="formulas[index]"
            class="form-control form-control-lg"
            v-on:keydown.enter.prevent
          />
          <button v-on:click="addFormulaInput($event)">+</button>
          <button v-on:click="removeFormulaInput($event,index)">-</button>
        </div>
      </section>
    </form>
    <VueCanvas :formulas="visibleFormulas" />
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
      visible: [false]
    };
  },
  computed: {
    visibleFormulas() {
      const res = [];
      for (const [index, formula] of this.formulas.entries()) {
        if (this.visible[index]) res.push(formula);
      }
      return res;
    }
  },
  methods: {
    addFormulaInput(e) {
      this.visible.push(false);
      this.formulas.push("");
      e.preventDefault();
    },
    removeFormulaInput(e, index) {
      if (this.formulas.length > 1) {
        this.visible.splice(index, 1);
        this.formulas.splice(index, 1);
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
  margin-top: 60px;
}
</style>
