<template>

  <AppHeader :totalIncome="state.totalIncome" />
  <AppForm :state="state" @add-income="AddIncome" />
  <FinanceList :state="state" @remove-item="removeItem" />
</template>

<script>
import { reactive, computed } from 'vue';
import AppHeader from './components/AppHeader';
import AppForm from './components/AppForm';
import FinanceList from './components/FinanceList';

export default {
  components: {
    AppHeader,
    AppForm,
    FinanceList,
  },
  setup() {

  const state = reactive({
    income: [],
    sortedIncome: computed(() => state.income.toSorted((a, b) => b.date - a.date)),
    totalIncome: computed(() => {
      if (state.income.length > 0) {
        return state.income.reduce((sum, item) => sum + item.value, 0);
      }
      return 0;
    })
  });

  function AddIncome(obj) {
    let d = obj.date.split("-");
    let newD = new Date(d[0], d[1], d[2]);

    state.income = [
      ...state.income,
      {
        id: Date.now(),
        desc: obj.desc,
        value: parseInt(obj.value),
        date: newD.getTime()
      }
    ];
  }

    function removeItem(id) {
  

  

  state.income = state.income.filter(item => item.id !== id);



}
  

  
  return {
    state,
    AddIncome,
    removeItem
  };
  
},
mounted() {
    document.title = "Controle de Finanças";
  }
};


</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
</style>