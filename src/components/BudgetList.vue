<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <template v-if="!isEmpty">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-comment">{{ item.comment }}</span>
          <span class="budget-value">{{ item.value }}</span>
          <ElButton type="danger" size="mini" @click="deleteItem(item.id)">Delete</ElButton>
        </div>
      </template>
      <ElAlert type="info" :title="emptyTitle" :closable="false" v-else />
    </ElCard>
  </div>
</template>

<script>
export default {
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      default: () => ({}),
    }
  },
  data: () => ({
    header: "Budget list",
    emptyTitle: "Empty list",
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    },
  },
}
</script>

<style scoped>
  .budget-list-wrap {
    max-width: 500px;
    margin: auto;
  }

  .list-item {
    display: flex;
    align-items: center;
    padding: 10px 15px;
  }

  .budget-value {
    font-weight: 600;
    margin-left: auto;
    margin-right: 20px;
  }
</style>
