<template>
  <div class="Home">
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

.Home {
  background-color: #13263c;
}

.Intro {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
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
