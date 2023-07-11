<template>
  <transition
    name="modal"
    appear>
    <div
      class="modal_v modal__dim"
      @click.self="$emit('close')">
      <div class="modal__content">
        <p class="modal__text">
          <slot name="modal-text"></slot>
        </p>
        <button
          class="clear"
          @click="clearTodo">
          예 :)
        </button>
        <button
          class="modal__close"
          @click="$emit('close')"
          @keyup.enter="$emit('close')"
          tabindex="0">
          아니요 X-X
        </button>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  emits: ["close","clearAll"],
  methods: {
    clearTodo() {
      // 초기화 후 새로고침
      location.reload()
      this.$emit("clearAll")
    }
  }
}
</script>

<style lang="scss" scoped>
.modal_v {
  width: 300px;
  height: 150px;
  background-color: rgba(255,255,255,.7);
  backdrop-filter: blur(3px);
  border: 3px solid $gray-200;
  border-radius: 10px;
  position: fixed;
  top: 25%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9;
  .modal__text {
    width: 200px;
    margin: 0 auto;
    margin-top: 40px;
    margin-bottom: 30px;
    slot {
      width: 50%;
    }
  }
  .clear, .modal__close {
    color: $gray-600;
    border: none;
    background-color: transparent;
    padding: 10px;
    &:hover {
      color: $black;
    }
  }
  @include media-breakpoint-down(md) {
    top: 50%;
  }
  @include media-breakpoint-down(sm) {
    width: 230px;
    height: 170px;
  }
}
</style>