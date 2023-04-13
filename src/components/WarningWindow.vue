<script>
import ButtonElement from "./ButtonElement.vue";

export default {
  components: {
    ButtonElement,
  },
  props: {
    isActive: {
      type: Boolean,
      // default: false,
    },
  },
  data() {
    return {
      buttons: [
        { name: "Continue", method: () => console.log("continue") },
        { name: "Cancel", method: this.closeWarningWindow },
      ],
      isWWActive: this.isActive,
    };
  },
  methods: {
    Clean() {
      console.log("clean");
    },
    closeWarningWindow() {
      this.isWWActive = false;
    },
  },
};
</script>

<template>
  <div class="warning-wrapper" :class="{ active: isWWActive }">
    <div class="warning-window">
      <div class="warning-window__header">
        <button class="btn-close" @click="closeWarningWindow">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="16"
            height="16"
            fill="currentColor"
            class="btn-close__icon"
            viewBox="0 0 16 16"
          >
            <path
              d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z"
            />
          </svg>
        </button>
      </div>
      <div class="warning-window__body">
        <p class="warning-window__text">data will be deleted. continue?</p>
        <div class="warning-window__confirm">
          <button-element
            v-for="btn in buttons"
            :title="btn.name"
            @click="btn.method"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.warning-wrapper {
  display: none;
}

.warning-wrapper.active {
  display: flex;
  position: absolute;
  top: 0;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.6);
  z-index: 100;
}

.warning-window {
  z-index: 2;
  background-color: white;
  border-radius: 2px;
  width: 336px;
}

.warning-window__header {
  padding: 12px;
  display: flex;
  justify-content: flex-end;
  border-bottom: 1px solid #808080;
}

.warning-window__body {
  display: flex;
  flex-direction: column;
  text-align: center;
  padding: 24px;
  gap: 24px;
}

.warning-window__confirm {
  display: flex;
  justify-content: center;
  gap: 24px;
}

.btn-close {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 8px;
  border: none;
  border-radius: 2px;
  background: none;
}

.btn-close:hover {
  background: #eeeeee;
}

.btn-close__icon {
  color: #808080;
}
</style>
