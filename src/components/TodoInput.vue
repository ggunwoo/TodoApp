<template>
  <div class="add">
    <div class="in__container">
      <input
        type="text"
        class="add__input"
        placeholder="Enter를 눌러주세요."
        v-model="newTodoItem"
        @keypress.enter="addTodoItem" />
      <button
        class="add__button"
        @click="addTodoItem">
        <span class="material-symbols-outlined">add</span>
      </button>
    </div> 
  </div>
</template>

<script>

export default {
  data() {
    return {
      newTodoItem: "",
    }
  },
  emits: ["addItem"],
  created() {
    const reps = window.matchMedia("screen and (max-width: 612px)")
    if(reps.matches) {
      console.log("모바일 사이즈")
    } else {
      console.log("모바일 사이즈 아닙니다.")
    }
  },
  methods: {
    addTodoItem() {
      if (this.newTodoItem !== "" || this.newTodoItem == "") {
        this.$emit("addItem", this.newTodoItem)
        this.clearInput()
      }
    },
    clearInput() {
      this.newTodoItem = ""
    }
  }
}
</script>
<style lang="scss" scoped>
.add {
  padding-bottom: 50px;
  .in__container {
    display: flex;
    justify-content: center;
    align-items: center;
    .add__input {
      width: 80%;
      height: 48px;
      margin-right: 20px;
      padding-left: 10px;
      border: none;
      border-radius: 5px;
    }
    button.add__button {
      width: 20%;
      height: 48px;
      background: $white;
      border: none;
      border-radius: 5px;
    }
  }
  @include media-breakpoint-down(md) {
    .in__container {
      .add__input {
        &::placeholder {
          font-size: 0;
        }
      }
    }
  }
}
</style>