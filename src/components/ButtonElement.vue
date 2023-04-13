<script>
export default {
  props: {
    title: {
      type: String,
      default: "click here",
    },
  },
  methods: {
    click() {
      this.$emit("click");
    },
  },
};
</script>

<template>
  <button class="button">{{ title }}</button>
</template>

<style>
.button {
  background: #3478f7;
  border: none;
  border-radius: 18px;
  color: white;
  line-height: 36px;
  padding: 0 18px;
  cursor: pointer;
  width: 100px;
  font-size: inherit;
}
.button:hover {
  filter: brightness(85%);
  /* backdrop-filter: brightness(80%); */
}
</style>
