<template>
  <div class="list-item">
    <span class="budget-comment">{{ item.comment }}</span>
    <span class="budget-value">{{ item.value }}</span>
    <ElButton type="danger" size="mini" @click="deleteItem(item.id)">Delete</ElButton>
  </div>
</template>

<script>
  export default {
    name: "BudgetListItem",
    props: {
      item: {
        type: Object,
        default: () => ({}),
      }
    },
    methods: {
      deleteItem(id) {
        if(confirm('Вы точно хотите удалить запись ?')) {
          this.$emit('deleteItemToList', id);
        }
      },
    },
  }
</script>

<style scoped>
  .list-item {
    display: flex;
    align-items: center;
    padding: 10px 20px;
  }

  .budget-value {
    font-weight: 600;
    margin-left: auto;
    margin-right: 20px;
  }
</style>
