<template>
  <div id="app">
    <div class="container">
      <Score :score="cakes.length" />
      <Cupcake
        @cupclick="clickHandler(cake, $event)"
        v-for="(cake, i) in cakes"
        :key="i"
        v-bind="cake"
      />
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

export default {
  name: "App",
  components: {
    Cupcake,
    NomNom,
    Score,
  },
  methods: {
    clickHandler(cake, event) {
      let cakeCopy = [...this.cakes];
      let index = this.cakes.indexOf(cake);
      cakeCopy.splice(index, 1);
      this.cakes = cakeCopy;
      let audio = new Audio("blop.mp3");
      audio.play();
      this.nomnoms.push({
        x: `${event.clientX}px`,
        y: `${event.clientY}px`,
      });
      setTimeout(() => {
        this.nomnoms.splice(0, 1);
      }, 2000);
    },
  },
  created() {
    // let cupcakeWidth = 60;
    let windowWidth = window.innerWidth;

    let amountCupcakesLayers = Math.floor(Math.min(10, windowWidth / 60));
    // let faktor = 5; // TODO based on max amountCupcakeLayers
    // for (let layer = 0; layer < amountCupcakesLayers; layer++) {
    //   console.log("layer", layer);
    //   let x = layer * 10;
    //   let amountCupcakesOnCurrentFloor = amountCupcakesLayers - layer;
    //   for (let cup = 0; cup < amountCupcakesOnCurrentFloor; cup++) {
    //     let y = 5 + faktor * cup;
    //     console.log(cup);
    //     this.cakes.push({ x: `${x}%`, y: `${y}%` });
    //   }
    // }
    let cakeAmount = 0;
    for (let row = 0; row < amountCupcakesLayers; row++) {
      let y = row * 10;
      for (let cake = 0; cake < amountCupcakesLayers - row; cake++) {
        let x = windowWidth / 3 + row * 30 + cake * 60;
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
  data: () => {
    return {
      cakes: [],
      nomnoms: [],
      score: 0,
      maxScore: 0,
    };
  },
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
  background-color: black;
}
</style>
