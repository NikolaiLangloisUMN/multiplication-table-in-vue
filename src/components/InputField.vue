<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    required: true,
  },
  labelCopy: {
    type: String,
    required: true,
  },
  min: {
    type: Number,
    required: false,
  },
  max: {
    type: Number,
    required: false,
  }
})

const model = defineModel()
</script>

<template>
  <label :id="name">
    <span v-html="labelCopy"/>
    <input :id="name" :type="type" :min="min" :max="max" v-model="model"/>
  </label>
</template>

<style scoped>
label {
  display: flex;
  justify-content: space-between;
  column-gap: 20px;
  align-items: center;

  input {
    font-size: 1rem;

    &[type='text'] {
      text-align: center;
    }
  }
}
</style>