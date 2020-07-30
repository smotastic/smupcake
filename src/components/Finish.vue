<template>
  <div class="container">
    <div>Congratulations, you just ate {{cupcakesAte}} Cupcakes.</div>
    <div>I hope you are proud of yourself</div>
    <div></div>
    <div
      class="pt"
    >This amounts to about {{calories}} Calories or {{daysWorthOfCalories}} days worth of eating.</div>
    <div class="pt">
      <a @click="reload" href="#">So lets eat again!</a>
    </div>
    <div>It's cupcakes after all, what could go wrong?</div>
  </div>
</template>

<script>
export default {
  props: {
    cupcakesAte: Number
  },
  methods: {
    clickHandler() {
      console.log("i dont know");
    },
    reload() {
      location.reload();
    }
  },
  computed: {
    calories() {
      return this.cupcakesAte * 200;
    },
    daysWorthOfCalories() {
      return this.calories / 2000;
    }
  }
};
</script>

<style scoped>
.container {
  margin: auto;
  text-align: center;
  margin-top: 10%;
  font-size: 25pt;
}
.container > div {
  color: white;
}
a {
  color: white;
}
.pt {
  padding-top: 20px;
}
</style>