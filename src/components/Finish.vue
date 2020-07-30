<template>
  <div class="container">
    <div>Congratulations, you just ate {{cupcakesAte}} Cupcakes.</div>
    <div>I hope you are proud of yourself</div>
    <div></div>
    <div class="pt">
      Want to know more of the Cupcakes you just ate?
      <a href="#" @click="clickHandler">Click</a>
    </div>
    <transition name="bounce">
      <Picture v-if="show" />
    </transition>
    <div v-if="showText">Spass, es war ein sehr gutes Projekt. Ich hoffe wir sehen uns bald mal wieder!</div>
    <!-- <div class="pt">
      <a @click="reload" href="#">So lets eat again!</a>
    </div>
    <div>It's cupcakes after all, what could go wrong?</div>-->
  </div>
</template>

<script>
import Picture from "./Picture";
export default {
  components: {
    Picture
  },
  props: {
    cupcakesAte: Number
  },
  methods: {
    clickHandler() {
      this.show = true;
      console.log("i dont know");
      setTimeout(() => {
        this.showText = true;
      }, 1000);
    },
    reload() {
      location.reload();
    }
  },
  data: () => {
    return {
      show: false,
      showText: false
    };
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

.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 1s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0) rotate(0deg);
  }
  50% {
    transform: scale(4) rotate(180deg);
  }
  100% {
    transform: scale(1) rotate(360deg);
  }
}
</style>