<template>
  <div id="app">
<<<<<<< HEAD
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
        </div>
      </section>
    </form>
    <VueCanvas :formulas="visibleFormulas" />
=======
    <h1>Math function drawing</h1>
    <VueCanvas />
>>>>>>> 5ffd5b842108b42ae4bb52610662e2e2630f4e17
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
