<template>
  <Header :totalIncome = state.totalIncome />
  <Forms @addIncome = addIncome />
  <IncomeList :state= state @remove-item="removeItem"/>
</template>

<script>
import { defineComponent, reactive, computed } from "vue";
import Header from './components/Header';
import Forms from "./components/Forms";
import IncomeList from "./components/IncomeList"

export default defineComponent ({
  components: {
    Header,
    Forms,
    IncomeList
  },
  setup() {
    const state = reactive({
      income : [],
      sortedIncome: computed(() => {
        let newArray = [];
        let sortIncome = state.income
        newArray = sortIncome.sort(function (a, b) {
          return b.date - a.date;
        });
        return newArray;
      }),
      totalIncome: computed(() => {
        let temp = 0;
        for (let i = 0; i<state.income.length; i++) {
          temp += state.income[i].value;
        }
        return temp;
      }),
    });
    function addIncome(obj) {
      let d = obj.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);
      state.income = [...state.income, {
        id: Date.now(),
        desc: obj.desc,
        value: parseInt(obj.value),
        date: newD.getTime()
      }]
      console.log("state.income", state.income);
    }

    function removeItem(id) {
      state.income = state.income.filter(v => v.id != id);
    }

    return {
      state,
      addIncome,
      removeItem,
    }
  },
})
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}
body {
  background: #EEE;
}
</style>
