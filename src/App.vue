<template>
  <div
    class="container">
    <div class="bgc_gr">
      <TodoHeader
        :propstime="nowTime" />
      <div v-if="userName">
        <TodoTitle
          :propsdata="checkCount"
          :propname="userName"
          @changeName="addUserName" />
        <TodoInput 
          @addItem="addOneItem" />
      </div>
      <div v-else>
        <TodoHello
          @addName="addUserName" />
      </div>
    </div>
    <div
      class="bottom_bgc"
      v-if="userName">
      <TodoController
        @sortItem="sortAllItem"
        @allClear="StorageClearAll" />
      <TodoList 
        :propsdata="todoItems"
        :propempty="isEmpty"
        @removeItem="removeOneItem"
        @toggleItem="toggleOneItem" />
      <TodoFooter />
    </div>
    <Modal
      v-show="showModal"
      @close="showModal = false">
      <template #modal-text>
        {{ modalText }}
      </template>
    </Modal>
    <ClearModal
      v-show="clearModal"
      @close="clearModal = false"
      @clearAll="clearAllItem">
      <template #modal-text>
        {{ modalText }}
      </template>
    </ClearModal>
  </div>
</template>

<script>
import TodoHeader from "~/components/TodoHeader";
import TodoTitle from "~/components/TodoTitle";
import TodoInput from "~/components/TodoInput";
import TodoHello from "~/components/TodoHello";
import TodoController from "~/components/TodoController";
import TodoList from "~/components/TodoList";
import TodoFooter from "~/components/TodoFooter";
import Modal from "~/components/common/Modal";
import ClearModal from "~/components/common/ClearModal";

import getDate from "~/commonJS/getDate"

export default {
  components: {
    TodoHeader,
    TodoTitle,
    TodoInput,
    TodoHello,
    TodoController,
    TodoList,
    TodoFooter,
    Modal,
    ClearModal
  },
  data() {
    return {
      todoItems: [],
      userName: "",
      showModal: false,
      clearModal: false,
      modalText: "",
      nowTime: ""
    };
  },
  created() {
    this.userName = localStorage.getItem("userName")

    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (
          localStorage.key(i) !== "loglevel:webpack-dev-server" &&
          localStorage.key(i) !== "csCursors" &&
          localStorage.key(i) !== "csPointers" &&
          localStorage.key(i) !== "userName"
          ) {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          )
        }
      }
    }
  },
  methods: {
    // addItem
    addOneItem(todoItem) {
      // 빈 내용
      if (todoItem === '') {
        this.showModal = !this.showModal;
        this.modalText = "할 일을 입력해주세요!";
        return false;
      }
      // 중복
      for (let i = 0; i < this.todoItems.length; i++) {
        if (this.todoItems[i].item === todoItem) {
          this.showModal = !this.showModal
          this.modalText = "목록에 이미 있습니다!"
          return false
        }
      }
      var value = {
        item: todoItem,
        date: `${getDate().month}.${getDate().day}. ${getDate().week}`,
        time: getDate().time,
        completed: false
      }
      localStorage.setItem(todoItem, JSON.stringify(value))
      this.todoItems.push(value)
    },
    // removeItem
    removeOneItem(todoItem, index) {
      localStorage.removeItem(todoItem.item)
      this.todoItems.splice(index, 1)
    },
    // toggleItem
    toggleOneItem(todoItem) {
      todoItem.completed = !todoItem.completed
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
    },
    // addName
    addUserName(userName) {
      localStorage.setItem("userName", userName)
      this.userName = userName
    },
    // clearAll
    clearAllItem() {
      this.todoItems = []
      localStorage.clear()
    },
    // allClear
    StorageClearAll() {
        this.clearModal = !this.clearModal;
        this.modalText = "모든 데이터가 초기화 됩니다. 초기화 하시겠습니까?";
        return false;
    },
    // sortItem
    sortAllItem(onePick) {
      if (onePick.value === "date-desc") {
        this.sortTodoLatest()
      } else if (onePick.value === "date-asc") {
        this.sortTodoOldest()
      }
    },
    // sortAllItem()
    sortTodoLatest() {
      this.todoItems.sort(function(a, b) {
        return b.time - a.time;
      });
    },
    // sortAllItem()
    sortTodoOldest() {
      this.todoItems.sort(function(a, b) {
        return a.time - b.time;
      });
    },
    // propstime="nowTime"
    realTime() {
      this.nowTime = new Date().toLocaleTimeString('ko-KR', {
        dataStyle: 'short',
        hour: '2-digit',
        hourCycle: 'h12',
        minute: '2-digit',
        second: '2-digit',
      })
      setInterval(() => {
        this.nowTime = new Date().toLocaleTimeString('ko-KR', {
          dataStyle: 'short',
          hour: '2-digit',
          hourCycle: 'h12',
          minute: '2-digit',
          second: '2-digit',
        })
      }, 1000)
    }
  },
  mounted() {
    this.sortTodoOldest()
    this.realTime()
  },
  computed: {
    checkCount() {
      const checkLeftItems = () => {
        let leftCount = 0
        for (let i = 0; i < this.todoItems.length; i++) {
          if (this.todoItems[i].completed === false) {
            leftCount++
          }
        }
        return leftCount
      };

      const count = {
        total: this.todoItems.length,
        left: checkLeftItems()
      };
      return count
    },
    isEmpty() {
      return this.todoItems.length <= 0 ? true : false
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  text-align: center;
  background-color: $white;
  box-shadow: 8px 16px 16px hsl(0deg 0% 0% / .25);
  margin-top: 50px;
  margin-bottom: 100px;
  --border-width: 3px;
  padding-right: 0;
  padding-left: 0;
  
  // position: relative;
  // text-transform: uppercase;
  // border-radius: var(--border-width);

  // &::after {
  //   position: absolute;
  //   content: "";
  //   top: calc(-1 * var(--border-width));
  //   left: calc(-1 * var(--border-width));
  //   z-index: -1;
  //   width: calc(100% + var(--border-width) * 2);
  //   height: calc(100% + var(--border-width) * 2);
  //   background: linear-gradient(
  //     60deg,
  //     hsl(224, 85%, 66%),
  //     hsl(269, 85%, 66%),
  //     hsl(314, 85%, 66%),
  //     hsl(359, 85%, 66%),
  //     hsl(44, 85%, 66%),
  //     hsl(89, 85%, 66%),
  //     hsl(134, 85%, 66%),
  //     hsl(179, 85%, 66%)
  //   );
  //   background-size: 300% 300%;
  //   background-position: 0 50%;
  //   border-radius: calc(2 * var(--border-width));
  //   animation: moveGradient 4s alternate infinite;
  // }
  // @keyframes moveGradient {
  //   50% {
  //     background-position: 100% 50%;
  //   }
  // }
  .bgc_gr {
    background: linear-gradient(-45deg, #BB82FA, #7C7AF0, #A2CBFA);
    color: $white;
  }
  .bottom_bgc {
    // background-color: $white;
    // background-color: $gray-200;
    background-color: #F6F6FF;
  }
  @include media-breakpoint-down(md) {
    margin-top: 0;
    margin-bottom: 0;
    box-shadow: none;
  }
  @include media-breakpoint-down(sm) {}
}

</style>