<template>
  <header class="header">
    <div class="title">
      <p>My Todolist.</p>
    </div>
    <div class="date">
      <div class="month">
        {{ timemonth }}월&nbsp;
      </div>
      <div class="day">
        {{ timeday }}일&nbsp;
      </div>
      <div class="week">
        {{ timeweek }}요일
      </div>
      <div class="now__time">
        &nbsp;&nbsp;{{ this.propstime }}
      </div>
    </div>
  </header>
</template>

<script>
import getDate from "~/commonJS/getDate";

export default {
  data() {
    return {
      timeday: "",
      timemonth: "",
      timeweek: "",
      ampm: "",
    }
  },
  created() {
    this.timestamp = `${getDate().month}/${getDate().date} ${getDate().week}`
    this.timeday = `${getDate().day}`
    this.timemonth = `${getDate().month}`
    this.timeweek = `${getDate().week}`
  },
  props: ["propstime"]
}
</script>
<style lang="scss" scoped>
header {
  height: 50px;
  font-size: 1.125rem;
  margin: 0 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .title {
    font-weight: bold;
    font-family: 'Itim', sans-serif;
    p {
      margin-bottom: 0;
    }
  }
  .date {
    display: flex;
    font-size: 1rem;
    justify-content: flex-end;
    .day {}
    .month {}
    .week {}
    .now__time {}
  }
  @include media-breakpoint-down(md) {
    font-size: 15px;
    margin: 0 20px;
  }
  @include media-breakpoint-down(sm) {
    .title {
      p {}
    }
    .date {
      .now__time {
        display: none;
      }
    }
  }
}
</style>