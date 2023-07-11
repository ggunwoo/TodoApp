<template>
  <div class="title">
    <div class="in__container">
      <p class="title__text">
        <span class="title__message">
          {{ message }}<span class="ntt">&nbsp;&#58;&#41;&nbsp;</span> <!--ntt코드 :) -->
        </span>
        <span
          @keydown.enter="handleName"
          @blur="handleBlur"
          class="title__name"
          ref="test"
          spellcheck="false"
          contenteditable="true">
          {{ propname }}
        </span>
      </p>
      <p class="title__task">
        <span class="title__task-count">
          <em class="title__task-left">{{ propsdata.left }}<br /></em>
          <em class="titme__task-today">오늘 할 일</em>
        </span>
        <span class="title__task-info"></span>
      </p>
    </div>
  </div>
</template>

<script>
import getDate from "~/commonJS/getDate"

export default {
  props: ["propsdata", "propname"],
  data() {
    return {
      message: ""
    }
  },
  emits: ["changeName"],
  methods: {
    handleBlur(e) {
      const originalName = this.propname
      const newName = e.target.innerText
      if (newName !== originalName) {
        if (newName === "") {
          e.target.innerText = originalName
        } else {
          this.$emit("changeName", newName)
        }
      }
    },
    handleName() {
      this.$refs.test.blur();
    }
  },
  mounted() {
    this.message = getDate().daytime
  }
}
</script>

<style lang="scss" scoped>
.title {
  padding: 50px 0;
  .in__container {
    text-align: left;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .title__text {
      font-size: 28px;
      font-weight: bold;
      .title__message {}
      .title__name {}
    }
    .title__task {
      font-size: 16px;
      span.title__task-count {
        em.title__task-left {
          font-size: 28px;
        }
        em.title__task-today {}
      }
      span.title__task-info {}
    }
  }
  @include media-breakpoint-down(md) {
    .in__container {
      display: block;
      .title__text {
        .title__message {
          display: block;
          margin-bottom: 5px;
        }
      }
    }
  }
  @include media-breakpoint-down(sm) {
    .in__container {
      .title__text {
        width: 100%;
        .title__message {
          display: block;
          width: 100%;
          font-size: 24px;
        }
        .title__name {
          font-size: 24px;
        }
      }
      .title__task {
      font-size: 16px;
      span.title__task-count {
        em.title__task-left {
          font-size: 36px;
          font-weight: bold;
        }
        em.title__task-today {}
      }
      span.title__task-info {}
    }
    }
  }
}
</style>