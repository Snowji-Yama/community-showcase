<template>
  <div class="FlipCard" :class="formatedName" @click="flip">
    <div
      class="FlipCard-inner"
      :class="{ 'FlipCard-inner-clicked': isFlipped }"
    >
      <div class="FlipCard-front">
        {{ name }}
      </div>
      <div class="FlipCard-back">
        {{ name }}
      </div>
    </div>
  </div>
</template>

<script>
import eventBus from "../eventBus";

export default {
  name: "FlipCard",
  props: {
    name: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isFlipped: false,
    };
  },
  computed: {
    formatedName() {
      return this.name.toLowerCase().replaceAll(" ", "-");
    },
  },
  methods: {
    flip() {
      if (this.name === "placeholder") return;
      eventBus.$emit("RESET_FLIP", this.formatedName);
      this.isFlipped = !this.isFlipped;
      eventBus.$emit("SHOW_EMBED", !this.isFlipped ? null : this.name);
    },
  },
  mounted() {
    eventBus.$on("RESET_FLIP", (name) => {
      if (this.formatedName !== name) {
        this.isFlipped = false;
      }
    });
  },
};
</script>

<style scoped>
.FlipCard {
  background-color: transparent;
  width: 220px;
  height: 150px;
  perspective: 1000px;
  font-family: "Lobster", serif;
}

.FlipCard-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.FlipCard-inner-clicked {
  transform: rotateY(180deg);
}

.FlipCard-front,
.FlipCard-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.FlipCard-front {
  background-color: #bbb;
  color: black;
}

.FlipCard-back {
  background-color: dodgerblue;
  color: white;
  transform: rotateY(180deg);
}
</style>
