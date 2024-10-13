<template>
    <div class="income-list">
    <IncomeItem 
      v-for="data in state.sortedIncome" 
      :key="data.id" 
      :income="data" 
      @remove-item="$emit('remove-item', data.id)" 
    />
  </div>
</template>

<script>
import IncomeItem from './IncomeItem.vue';

export default {
  components: {
    IncomeItem
  },
  props: {
    state: Object
  },
  setup(props, { emit }) {
    
    return {
      emit
    };
  }
}

</script>

<style scoped>
 .income-list {
    margin-top: 30px;
    padding: 15px;
  }
</style>