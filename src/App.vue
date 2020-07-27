<template>
  <div id="app">
    <div class="container">
      <Cupcake v-for="(cake,i) in cakes" :key="i" v-bind="cake" />
    </div>
  </div>
</template>

<script>
import Cupcake from "./components/Cupcake.vue";

export default {
  name: "App",
  components: {
    Cupcake
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
        let x = row * 30 + cake * 60;
        cakeAmount++;
        setTimeout(() => {
          this.cakes.push({ x: `${x}px`, y: `${y}%` });
        }, cakeAmount * 100);
        // Math.max(1500 - cakeAmount * 40, 100)
      }
    }
  },
  data: () => {
    return {
      cakes: []
    };
  }
};
</script>

<style>
</style>
