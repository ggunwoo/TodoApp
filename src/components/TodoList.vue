<template>
  <div
    class="list"
    :class="listempty">
    <ul class="in__container">
      <li
        class="list__item"
        v-for="(todoItem, index) in propsdata"
        :key="todoItem.item">
        <input
          type="checkbox"
          class="checkbox"
          :id="todoItem.item"
          :checked="todoItem.completed === true"
          @change="toggleComplete(todoItem)" />
        <label
          :for="todoItem.item"
          class="list__label"
          spellcheck="false">
          <p
            class="list__text"
            spellcheck="false">{{ todoItem.item }}</p>
        </label>
        <p class="list__date">
          {{ todoItem.date }}
        </p>
        <button
          class="list__delete"
          @click="removeTodo(todoItem, index)">
          <!-- X -->
          <span class="material-symbols-outlined">delete_forever</span>
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["propsdata", "propempty"],
  emits: ["removeItem", "toggleItem"],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit("removeItem", todoItem, index)
    },
    toggleComplete(todoItem) {
      this.$emit("toggleItem", todoItem)
    }
  },
  computed: {
    listempty() {
      return this.propempty ? "list--empty" : null
    }
  }
}
</script>

<style lang="scss" scoped>
.list {
  .in__container {
    padding-left: 0;
    min-height: 300px;
    .list__item {
      width: 100%;
      min-height: 30px;
      height: 100%;
      padding: 10px 0;
      padding-left: 10px;
      margin-bottom: 20px;
      // padding-right: 20px;
      background-color: #fff;
      border-radius: 5px;
      display: flex;
      align-items: center;
      p {
        margin: 0;
      }
      &:last-child {
        margin-bottom: 0;
      }
      input {
        width: 5%;
        &[type="checkbox"] {
          width: 17px;
          height: 17px;
        }
      }
      .list__label {
        width: 70%;
        text-align: left;
        margin-left: 10px;
      }
      .list__date {
        width: 15%;
      }
      .list__delete {
        width: 5%;
        border: none;
        background-color: $white;
      }
    }
  }
  @include media-breakpoint-down(md) {
    .in__container{
      .list__item {
        p {
        }
        &:last-child {
        }
        input {
          width: 5%;
        }
        .list__label {
          width: 65%;
        }
        .list__date {
          width: 15%;
        }
        .list__delete {
          width: 5%;
        }
      }
    }
  }
  @include media-breakpoint-down(sm) {
    .in__container{
      .list__item {
        p {
        }
        &:last-child {
        }
        input {
          width: 5%;
        }
        .list__label {
          width: 50%;
        }
        .list__date {
          width: 20%;
        }
        .list__delete {
          width: 5%;
        }
      }
    }
  }
}
</style>