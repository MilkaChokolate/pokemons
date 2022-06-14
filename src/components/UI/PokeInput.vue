<template>
  <input placeholder="Search" :value="modelValue" @input="updateInput" class="input" type="text">
</template>

<script>
export default {
  name: 'my-input',
  props: {
    modelValue: String
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>
.input {
  width: 20%;
  min-width: 200px;
  border: 1px solid black;
  padding: 10px 15px;
  margin-top: 15px;
  border-radius: 5px;
}
</style>