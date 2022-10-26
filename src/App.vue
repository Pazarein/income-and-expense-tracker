<template>
 <MainHeader :totalIncome="state.totalIncome" />
 <MainForm  @add-income="AddIncome" />
 <IncomeListVue :state="state" @remove="remove"/>
</template>

<script>
import { reactive, computed } from 'vue';
import MainHeader from './components/MainHeader.vue';
import MainForm from './components/MainForm.vue';
import { toNumber } from '@vue/shared';
import IncomeListVue from './components/IncomeList.vue';

export default {
  components: {
    MainHeader,
    MainForm,
    IncomeListVue,
  },
  setup(){

    const state = reactive({
      income: [],
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        }
        
        return temp;

      }),
      sortedIncome: computed(() => {
        let temp = [];
        temp = state.income.sort( (a,b) => b.date - a.date)
        return temp;
      })
    })

    function AddIncome (data) {

      let d = data.date.split("-");
      let newD = new Date(d[0],d[1],d[2]);

      state.income = [...state.income, {
        id: Date.now(),
        desc: data.desc,
        value: toNumber(data.value),
        date: newD.getTime()
      }]
      console.log(state.income);
    }

    function remove(id) {
      state.income = state.income.filter(i => i.id !== id);
    }

    return {
      state, AddIncome, remove
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}
body {
  background: rgb(210, 220, 208);
}
</style>
