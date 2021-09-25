<template>
  <div class="CardList">
    <img src="../assets/title.png" alt="title" class="title" />

    <div class="CardList-cards">
      <div class="CardList-card" v-for="embed in embeds" :key="embed.name">
        <flip-card :name="embed.name" />
      </div>
      <div v-if="embeds.length % 2 !== 0" class="CardList-card">
        <flip-card class="placeholder" name="placeholder" />
      </div>
    </div>

    <embed-panel />
  </div>
</template>

<script>
import { EMBEDS } from "../embeds";

import FlipCard from "./FlipCard";
import EmbedPanel from "./EmbedPanel";

export default {
  name: "CardList",
  components: {
    FlipCard,
    EmbedPanel,
  },
  computed: {
    embeds() {
      return EMBEDS;
    },
  },
};
</script>

<style scoped>
.CardList {
  display: flex;
  flex-direction: column;
  align-items: center;
  /*background-color: #13263c;*/
  min-height: 100vh;
  width: 100vw;
}

.CardList .title {
  height: 200px;
}

.CardList .CardList-cards {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  width: 100vw;
  padding-bottom: 200px;
}

.CardList .CardList-cards .CardList-card {
  margin-bottom: 15px;
  margin-right: 15px;
}
.CardList .CardList-cards .CardList-card .placeholder {
  opacity: 0;
}
</style>
