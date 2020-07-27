<template>
  <div class="cupcake" :style="{left: this.x, bottom: this.y}">
    <div class="frosting">
      <span class="cherry"></span>
      <span class="top"></span>
      <span class="middle"></span>
      <span class="bottom"></span>
    </div>
    <div class="cake"></div>
    <div class="cup">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    x: String,
    y: String
  }
};
</script>

<style scoped>
.cupcake {
  width: 60px;
  position: absolute;
  font-size: 0;
  bottom: 0;
}
.cake {
  width: 60px;
  height: 8px;
  background-color: #322421;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}
.cup {
  width: 60px;
  height: 0;
  border: solid;
  border-width: 40px 0 0 0;
  border-color: #a4d2de transparent transparent;
  border-bottom-left-radius: 26px 40px;
  border-bottom-right-radius: 26px 40px;
  position: relative;
  display: inline-block;
  z-index: 0;
}
.cup span {
  height: 10px;
  width: 15px;
  display: inline-block;
  background-color: #a4d2de;
  position: relative;
  top: -42px;
  border-radius: 50%;
  margin: 0;
}
.cup span:after {
  content: "";
  top: 6px;
  position: absolute;
  width: 1px;
  height: 30px;
  background-color: rgba(255, 255, 255, 0.6);
  transform: rotate(0deg);
}
.cup span:first-child:after {
  background-color: transparent;
}
.frosting span {
  display: block;
  position: relative;
  height: 8px;
  margin: auto;
  background-color: #ff7fbf;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  border-top: 1px solid pink;
}
.frosting span.bottom {
  width: 51px;
}
.frosting span.middle {
  width: 39px;
}
.frosting span.top {
  width: 27px;
}
.frosting span.cherry {
  box-sizing: border-box;
  border-top: 0;
  width: 8px;
  border-radius: 50%;
  background-color: white;
  box-shadow: -1px -1px 0px 3px #c40000 inset;
}
</style>