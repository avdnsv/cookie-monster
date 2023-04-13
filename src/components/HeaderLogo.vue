<script>
import IconLogo from "./icons/IconLogo.vue";

export default {
  components: {
    IconLogo,
  },
};
</script>

<template>
  <div class="header-app">
    <icon-logo />
    <h1 class="name-app">Welcome to Cookie Monster</h1>
  </div>
</template>

<style>
.header-app {
  text-align: center;
  padding: 24px 24px 16px;
}

.name-app {
  font-size: inherit;
  margin-top: 8px;
  color: white;
}
</style>
