<template>
  <div id="app">
    <FormBudget />
    <TotalBalance :total="totalBalance" />
    <BudgetList :list="list" @deleteItem="onDelete" />
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
import FormBudget from '@/components/FormBudget';
export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    FormBudget,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      }
    },
  }),
  computed: {
    totalBalance() {
      let balance = Object.values(this.list).reduce(function(sum, el) {
        return sum + el.value
      }, 0);
      return balance
    },
  },
  methods: {
    onDelete(id) {
      this.$delete(this.list, id);
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
