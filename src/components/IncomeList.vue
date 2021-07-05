<template>
  <div class="income-list">
    <incomeItem v-for="data in state.sortedIncome" :key="data.id" :income="data" @remove-item="removeItem"/>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import incomeItem from './IncomeItem.vue';
export default defineComponent ({
  components: {
    incomeItem,
  },
  props:{
    state: Object,
  },
  setup (props, { emit }) {
    function removeItem(id) {
      emit( 'remove-item', id );
    }
    return {
      incomeItem,
      removeItem
    }
  }
})
</script>

<style scoped>
  .income-list {
    margin-top: 30px;
    padding: 15px;
  }
</style>