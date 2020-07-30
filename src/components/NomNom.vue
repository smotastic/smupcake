<template>
  <div :style="{left: this.x, top: this.y}">Nom Nom</div>
</template>

<script>
export default {
  props: {
    x: String,
    y: String,
  },
};
</script>

<style scoped>
div {
  position: absolute;
  font-weight: bold;
  font-size: 26pt;
  color: white;
}
</style>