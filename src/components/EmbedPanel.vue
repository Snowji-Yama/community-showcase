<template>
  <div v-if="visible" class="EmbedPanel">
    <div v-html="embed" />
  </div>
</template>

<script>
import eventBus from "../eventBus";
import { EMBEDS } from "../embeds";

export default {
  name: "EmbedPanel",
  data() {
    return {
      visible: false,
      embed: "",
    };
  },
  mounted() {
    eventBus.$on("SHOW_EMBED", (name) => {
      if (!name) {
        this.visible = false;
        this.embed = "";
      }

      const embedData = EMBEDS.find((embed) => embed.name === name);
      this.embed = embedData.embed;
      this.visible = true;
    });
  },
};
</script>

<style scoped>
.EmbedPanel {
  position: fixed;
  bottom: 0;
  width: 600px;
  background: white;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}
</style>
