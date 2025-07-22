<template>
  <ElCard class="form-card">
    <ElForm :model='formData'>
      <ElFormItem label="Type" prop="type">
        <ElSelect class="type-select" v-model="formData.type" placeholder="chose type...">
          <ElOption label="Income" value="INCOME" />
          <ElOption label="Outcome" value="OUTCOME" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comment" prop="comment">
        <ElInput v-model="formData.comment" />
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value" />
      </ElFormItem>
      <ElButton type="primary" @click.prevent="onSubmit">Submit</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  name: 'FormBudget',
  data: ()=>({
    formData: {
      type: 'INCOME',
      comment: '',
      value: 0,
    },
  }),
  methods: {
    onSubmit() {

    },
  }
}
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}

.type-select {
  width: 100%;
}
</style>
