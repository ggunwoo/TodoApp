<template>
  <div class="helloCtn">
    <div>
      <div class="hello">
        사용자 이름을 입력해주세요
      </div>
      <!-- <label for="user-name"></label> -->
      <input
        type="text"
        id="user-name"
        v-model="userName"
        @keyup.enter="addUserName()" />
      <button
        class="btn__addName"
        @click="addUserName()">
        반가워요&nbsp;&#58;&#41;
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userName: ""
    };
  },
  emits: ["addName"],
  methods: {
    addUserName() {
      this.$emit("addName", this.userName);
    }
  }
};
</script>
<style lang="scss" scoped>
.helloCtn {
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
  .hello {
    margin-bottom: 20px;
  }
  input#user-name {
    font-size: 18px;
    border: none;
  }
  .btn__addName {
    font-size: 12px;
    font-family: GmarketSansbold;
    display: block;
    margin: 0 auto;
    border: none;
    background: $white;
    margin-top: 20px;
    padding: 7px 15px;
    border-radius: 7px;
  }
  @include media-breakpoint-down(md) {
    height: calc(100vh - 50px);
    input#user-name {
      font-size: 16px;
      height: 36px;
    }
  }
}
</style>