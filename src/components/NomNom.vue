<template>
  <div :style="{left: this.x, top: this.y}">{{shownNom}}</div>
</template>

<script>
export default {
  props: {
    x: String,
    y: String
  },
  created() {
    this.shownNom = this.nomnoms[
      Math.floor(Math.random() * this.nomnoms.length)
    ];
  },
  data: () => {
    return {
      nomnoms: [
        "Nom nom",
        "Meinem Gaumen gefällts",
        "Welch Geschmackserlebnis",
        "Liegt gut auf der Zunge",
        "Welcher Bäcker hat diese gottesgleichen Miniaturtörtchen hergestellt?",
        "MEHR, so bringet er mir mehr!",
        "Hmm.. legga"
      ],
      shownNom: ""
    };
  }
};
</script>

<style scoped>
div {
  position: absolute;
  font-weight: bold;
  font-size: 34pt;
  color: white;
  -webkit-text-stroke: 1px black; /* width and color */
}
</style>