<template>
  <div id="app">
    <div class="container">
      <Cupcake
        @cupclick="clickHandler(cake, $event)"
        v-for="(cake, i) in cakes"
        :key="i"
        v-bind="cake"
      />
      <Score v-if="!finished" :score="cakes.length" :initialFirstRow="amountCupcakesLayers" @cupchange="cupAmountChanged($event)" />
      <Finish v-if="finished" :cupcakesAte="maxCupcakes" />
      <transition-group name="fade">
        <NomNom v-for="(nom) in nomnoms" :key="nom.x" v-bind="nom" />
      </transition-group>
    </div>
  </div>
</template>

<script>
import Cupcake from "./components/Cupcake.vue";
import NomNom from "./components/NomNom.vue";
import Score from "./components/Score.vue";
import Finish from "./components/Finish.vue";

export default {
  name: "App",
  components: {
    Cupcake,
    NomNom,
    Score,
    Finish
  },
  methods: {
    cupAmountChanged(event) {
      this.amountCupcakesLayers = parseInt(event.target.value);
      this.redo();
    },
    clickHandler(cake, event) {
      this.ateAtLeastOne = true;
      let cakeCopy = [...this.cakes];
      let index = this.cakes.indexOf(cake);
      cakeCopy.splice(index, 1);
      this.cakes = cakeCopy;
      let audio = new Audio("blop.mp3");
      audio.play();
      this.nomnoms.push({
        x: `${event.clientX}px`,
        y: `${event.clientY}px`
      });
      setTimeout(() => {
        this.nomnoms.splice(0, 1);
      }, 2000);
    },
    calc() {
      this.ateAtLeastOne = false;
      let windowWidth = window.innerWidth;

      //Math.floor(Math.min(10, windowWidth / 60));
      let startX = (windowWidth - this.amountCupcakesLayers * 60) / 2;
      this.maxCupcakes =
        (this.amountCupcakesLayers * (this.amountCupcakesLayers + 1)) / 2;

      let cakeAmount = 0;
      for (let row = 0; row < this.amountCupcakesLayers; row++) {
        let y = 5 + row * 10;
        for (let cake = 0; cake < this.amountCupcakesLayers - row; cake++) {
          let x = startX + row * 30 + cake * 60;
          cakeAmount++;
          setTimeout(() => {
            this.cakes.push({ x: `${x}px`, y: `${y}%` });
            let audio = new Audio("blop.mp3");
            audio.play();
          }, cakeAmount * 100);
          // Math.max(1500 - cakeAmount * 40, 100)
        }
      }
    },
    redo() {
      this.cakes = [];
      this.calc();
    }
  },
  created() {
    this.calc();
  },
  data: () => {
    return {
      cakes: [],
      nomnoms: [],
      score: 0,
      maxScore: 0,
      ateAtLeastOne: false,
      maxCupcakes: null,
      amountCupcakesLayers: 6
    };
  },
  computed: {
    finished() {
      return this.ateAtLeastOne && this.cakes.length === 0;
    }
  }
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

body {
  background-color: #1b2f52;
}
</style>
