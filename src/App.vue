<template>
  <div id="app">
    <FormBudget @addNewItem="onNewItem" />
    <TotalBalance :total="totalBalance" />
    <BudgetSort @sortList="onSortList" />
    <BudgetList :list="sortListBudget" @deleteItem="onDelete" />
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
import FormBudget from '@/components/FormBudget';
import BudgetSort from '@/components/BudgetSort';
export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    FormBudget,
    BudgetSort,
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
    sortList: null,
  }),
  computed: {
    totalBalance() {
      let balance = Object.values(this.list).reduce(function(sum, el) {
        return sum + el.value
      }, 0);
      return balance
    },
    sortListBudget() {
      let list = {...this.list};
      if(this.sortList !== null) list = this.sortList;
      return list;
    },
  },
  watch: {
    list: "onSortList",
  },
  methods: {
    onDelete(id) {
      this.$delete(this.list, id);
    },
    onNewItem(item) {
      const newObj = {...item, id: String(Math.random())}
      this.$set(this.list, newObj.id, newObj);
    },
    onSortList(type = "ALL") {
      console.log(this.list);
      let sortList = Object.values(this.list).reduce((list, item)=>{
        if(item.type === type) {
          list[item.id] = item;
        } else if (type === 'ALL') list[item.id] = item;
        return list
      }, {})
      this.sortList = sortList;
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
