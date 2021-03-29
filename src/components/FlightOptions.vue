<template>
  <div class="options">
    <p class="options__title">Опции тарифа</p>
    <div class="options__checkbox">
      <input v-model="optionsFilters" value="onlyDirect" type="checkbox" id="onlyDirect" />
      <label for="onlyDirect">Только прямые</label>
    </div>
    <div class="options__checkbox">
      <input v-model="optionsFilters" value="withBaggage" type="checkbox" id="withBaggage" />
      <label for="withBaggage">Только с багажом</label>
    </div>
    <div class="options__checkbox">
      <input v-model="optionsFilters" value="onlyReturn" type="checkbox" id="onlyReturn" />
      <label for="onlyReturn">Только возвратные</label>
    </div>
  </div>
</template> 

<script>
export default {
  data() {
    return {
      optionsFilters: []
    }
  },
  watch: {
    optionsFilters: function() {
      this.$emit('clicked', this.optionsFilters)
    }  
  }
}
</script>

<style scoped>
.options {
  background-color: #f5f5f5;
  padding: 12px;
  border-radius: 4px;
  margin-bottom: 12px;
}
.options__title {
  font-weight: 700;
  margin-bottom: 12px;
  line-height: 20px;
}
.options__checkbox {
  display: flex;
  line-height: 16px;
  margin-bottom: 12px;
  font-size: 12px;

}
.options__checkbox:last-child {
  margin-bottom: 0;
}
.options__checkbox input[type=checkbox] {
  margin-right: 12px;
}
</style>