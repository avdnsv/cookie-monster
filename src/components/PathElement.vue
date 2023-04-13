<script>
export default {
  props: {
    path: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  methods: {
    sizing(res) {
      let sizes = ["KB", "MB", "GB", "TB"];
      if (res < 1024) return `${res} B`;
      let i = 0;
      while (res > 1024) {
        res = res / 1024;
        i++;
      }
      return `${res.toFixed(2)} ${sizes[i]}`;
    },
  },
};
</script>

<template>
  <div class="path">
    <component :is="path.icon"></component>
    <div class="path__wrapper">
      <p class="path__name-path">{{ path.name }}</p>
      <p class="path__quantity-path" v-if="path.quantity != 1">
        {{ path.quantity }} items,
      </p>
      <p class="path__quantity-path" v-else>{{ path.quantity }} item,</p>
      <p class="path__size-path">{{ sizing(path.size) }}</p>
    </div>
    <input class="path__is-include" type="checkbox" v-model="path.isInclude" />
  </div>
</template>

<style>
.path {
  display: flex;
  margin-bottom: 16px;
}

.path__quantity-path,
.path__size-path {
  display: inline;
  color: #808080;
}

.path:last-child {
  margin-bottom: 0;
}

.path__wrapper {
  width: 100%;
}

.path__icon {
  margin-right: 16px;
  height: auto;
  width: 24px;
  color: #808080;
}

.path__name-path {
  font-size: 15px;
}
.path__name-path_colored {
  color: #808080;
}
</style>
