<template>
  <div class="Home background">
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <transition name="fade" mode="out-in">
      <div v-if="!isHomeLoaded" class="Intro" @click="skipIntro" key="1">
        <!--<img src="../assets/background.jpg" alt="background" />-->
        <transition name="bounce">
          <img
            v-if="showTitle"
            src="../assets/title.png"
            alt="title"
            class="title"
          />
        </transition>
      </div>
      <div v-else key="2">
        <card-list />
      </div>
    </transition>
  </div>
</template>

<script>
import CardList from "./CardList";

export default {
  name: "Home",
  components: { CardList },
  data() {
    return {
      isHomeLoaded: false,
      showTitle: false,
    };
  },
  computed: {},
  methods: {
    skipIntro() {
      this.isHomeLoaded = true;
    },
  },
  mounted() {
    setTimeout(() => {
      this.showTitle = true;
    }, 500);
  },
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.bounce-enter-active {
  animation: bounce-in 1s;
}
.bounce-leave-active {
  animation: bounce-in 1s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1);
  }
  75% {
    transform: scale(0.9);
  }
  100% {
    transform: scale(1);
  }
}

.Intro {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  /*background-color: #13263c;*/
}
.Intro img {
  height: 100%;
  width: 100%;
}
.Intro .title {
  position: absolute;
}

.Intro:hover {
  cursor: pointer;
}
</style>

<style lang="scss" scoped>
/*body {
  margin: 0;
  overflow: hidden;
}*/

.background {
  width: 100vw;
  height: 100vh;
  background: #3e1e68;
}

$particleSize: 15vmin;
$animationDuration: 6s;
$amount: 20;
.background span {
  width: $particleSize;
  height: $particleSize;
  border-radius: $particleSize;
  backface-visibility: hidden;
  position: absolute;
  animation-name: move;
  animation-duration: $animationDuration;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  $colors: (#583c87, #e45a84, #ffacac);
  @for $i from 1 through $amount {
    &:nth-child(#{$i}) {
      color: nth($colors, random(length($colors)));
      top: random(100) * 1%;
      left: random(100) * 1%;
      animation-duration: (random($animationDuration * 10) / 10) * 1s + 10s;
      animation-delay: random(($animationDuration + 10s) * 10) / 10 * -1s;
      transform-origin: (random(50) - 25) * 1vw (random(50) - 25) * 1vh;
      $blurRadius: (random() + 0.5) * $particleSize * 0.5;
      $x: if(random() > 0.5, -1, 1);
      box-shadow: ($particleSize * 2 * $x) 0 $blurRadius currentColor;
    }
  }
}

@keyframes move {
  100% {
    transform: translate3d(0, 0, 1px) rotate(360deg);
  }
}
</style>
