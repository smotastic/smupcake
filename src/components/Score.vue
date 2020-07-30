<template>
  <div class="container">
    <div>Cupcakes: {{score}}</div>
    <div>Click to eat</div>
    <div v-if="score === 0">
      Congratulations, you just ate a ton of Cupcakes.
      <button @click="eatagain">Eat again?</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    score: Number,
  },
  created() {
    this.maxScore = this.score;
  },
  data: () => {
    return {
      maxScore: 0,
    };
  },
  methods: {
    eatagain() {
      location.reload();
    },
  },
};
</script>

<style scoped>
div.container {
  position: absolute;
  left: 75%;
  bottom: 85%;
  color: white;
}
</style>