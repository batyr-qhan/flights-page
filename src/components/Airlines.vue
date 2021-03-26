<template>
  <div class="airlines">
    <p class="airlines__title">Авиакомпании</p>
    <ul class="airlines__list">
      <li class="airlines__checkbox" v-for="(airline, name) in airlinesList" :key="name">
        <input type="checkbox" :id="airline" />
        <label :for="airline">{{ airline }}</label>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["airlinesList"],
};
</script>

<style scoped>
.airlines {
  background-color: #f5f5f5;
  padding: 12px;
  border-radius: 4px;
  height: 320px;
  display: flex;
  flex-direction: column;
}
.airlines__title {
  font-weight: 700;
  margin-bottom: 12px;
  line-height: 20px;
}
.airlines__list {
  overflow-y: scroll;
}
.airlines__checkbox {
  display: flex;
  line-height: 16px;
  margin-bottom: 12px;
  font-size: 12px;
}
.airlines__checkbox:last-child {
  margin-bottom: 0;
}
.airlines__checkbox input[type=checkbox] {
  margin-right: 12px;
}
</style>