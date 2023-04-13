<script>
import ButtonElement from "./ButtonElement.vue";

export default {
  components: {
    ButtonElement,
  },
  data() {
    return {
      buttons: [
        { name: "Analyse", method: this.analyse },
        { name: "Run Clean", method: this.warn },
      ],
    };
  },
  methods: {
    analyse() {
      // console.log("analyse");
      this.$emit("analyse");
    },
    warn() {
      console.log("warn");
      this.$emit("warn");
    },
  },
};
</script>

<template>
  <section class="buttons">
    <button-element
      v-for="btn in buttons"
      :title="btn.name"
      @click="btn.method"
    />
  </section>
</template>

<style>
.buttons {
  display: flex;
  justify-content: space-around;
}
</style>
