<template>
  <div class="ctrl">
    <div class="in__container">
      <div class="select">
        <select
          name="order"
          id="order"
          class="selectbox"
          v-model="onePick"
          @change="sortTodo">
          <option
            v-for="sortOption in sortOptions"
            :key="sortOption"
            :value="sortOption.value">
            {{ sortOption.txt }}
          </option>
        </select>
      </div>
      <button
        class="clear"
        @click="clearModalShow">
        초기화
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sortOptions: [
        {
          txt: "오래된순",
          value: "date-asc"
        },
        {
          txt: "최신순",
          value: "date-desc"
        },
      ],
      onePick : "date-asc"
    }
  },
  emits: ["sortItem", "allClear"],
  methods: {
    sortTodo() {
      this.$emit("sortItem", { value: this.onePick })
    },
    clearModalShow() {
      this.$emit("allClear")
    }
  }
}
</script>
<style lang="scss" scoped>
.ctrl {
  .in__container {
    height: 75px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .select {
      .selectbox {
        padding: 5px;
        border: none;
        border-radius: 5px;
      }
    }
    button.clear {
      color: $gray-500;
      background-color: $white;
      padding: 10px;
      border: none;
      border-radius: 5px;
      transition: all .2s;
      &:hover {
        color: $black;
      }
    }
  }
}
</style>