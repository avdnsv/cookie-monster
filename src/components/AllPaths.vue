<script>
import PathElement from "./PathElement.vue";
import AllButtons from "./AllButtons.vue";

import IconTrash from "./icons/IconTrash.vue";
import IconDownloads from "./icons/IconDownloads.vue";
import IconSafari from "./icons/IconSafari.vue";
import IconFile from "./icons/IconFile.vue";
import IconMailAtt from "./icons/IconMailAtt.vue";
import IconImessageAtt from "./icons/IconImessageAtt.vue";

import { markRaw } from "vue";

export default {
  components: {
    PathElement,
    AllButtons,
  },
  data() {
    return {
      paths: [
        {
          id: 0,
          name: "Trash",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconTrash),
        },
        {
          id: 1,
          name: "Downloads",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconDownloads),
        },
        {
          id: 2,
          name: "Safari (in progress)",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconSafari),
        },
        {
          id: 3,
          name: "Mail Attachements",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconMailAtt),
        },
        {
          id: 4,
          name: "iMessage Attachments (in progress)",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconImessageAtt),
        },
        {
          id: 5,
          name: "User Caches",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconFile),
        },
        {
          id: 6,
          name: "User Logs",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconFile),
        },
        {
          id: 7,
          name: "Global Temporary Files",
          quantity: 0,
          size: 0,
          isInclude: false,
          icon: markRaw(IconFile),
        },
      ],
    };
  },
  methods: {
    doAnalyse() {
      fetch("http://127.0.0.1:3310/analyse")
        .then((response) => response.json())
        .then((data) => {
          for (let path of this.paths) {
            for (let item of data) {
              if (path.id === item.id) {
                path.size = item.size;
                path.quantity = item.quantity;
              }
            }
          }
        });
    },

    doClean() {
      fetch("http://127.0.0.1:3310/clean", {
        method: "POST",
        headers: {
          "Content-Type": "application/json;charset=UTF-8",
        },
        body: JSON.stringify(
          this.paths.map((item) => {
            if (item.isInclude) {
              return { id: item.id };
            } else {
              return { id: 0 };
            }
          })
        ),
      }).then((response) => response.text());
    },

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
  computed: {
    totalQuantity() {
      return this.paths.reduce((total, path) => total + path.quantity, 0);
    },
    totalSize() {
      return this.paths.reduce((total, path) => total + path.size, 0);
    },
    totalSelectedSize() {
      let total = 0;
      for (let path of this.paths) {
        if (path.isInclude) {
          total += path.size;
        }
      }
      return total;
    },
  },
};
</script>

<template>
  <div class="main">
    <section class="paths">
      <path-element v-for="path in paths" :path="path" />
      <div class="path">
        <p class="path__name-path">
          Total:
          <span class="path__name-path_colored">
            {{ totalQuantity }} items, {{ sizing(totalSize) }}
          </span>
          &nbsp&nbsp&nbspSelected:
          <span class="path__name-path_colored">
            {{ sizing(totalSelectedSize) }}
          </span>
        </p>
      </div>
    </section>
    <all-buttons @analyse="doAnalyse" @warn="doClean" />
  </div>
</template>

<style>
.main {
  background: white;
  padding: 24px;
  border-radius: 32px 32px 0 0;
}

.paths {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
}
</style>
