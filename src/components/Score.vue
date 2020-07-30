<template>
  <div class="container">
    <div>Cupcakes: {{score}}</div>
    <div>Click to eat</div>
    <div>Or add more!
      <input :value="initialFirstRow" @change="$emit('cupchange', $event)" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    score: Number,
    initialFirstRow: Number
  },
  created() {
    this.maxScore = this.score;
  },
  data: () => {
    return {
      maxScore: 0
    };
  }
};
</script>

<style scoped>
div.container {
  position: absolute;
  left: 70%;
  bottom: 80%;
  color: white;
  font-size: 24pt;
}
</style>