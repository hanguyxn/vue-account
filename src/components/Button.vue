<script setup>
import { defineProps } from 'vue';
defineProps({
  onClick: Function,
  id: String,
  class: {
    type: String,
    default: "form-submit"
  },
  type: {
    type: String,
    default: "submit"
  },
  text: {
    type: String,
    default: "Click me!"
  }
})
</script>

<template>
  <button 
    class="form-submit" 
    :id="id" 
    :class="class" 
    :type="type" 
    @click="onClick" >
    {{ text }}
  </button>
</template>

<style scoped>
button.form-submit {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-bottom: 15px;
}

button.form-submit:hover {
  background-color: #0056b3;
}

button.form-submit:disabled {
  background-color: #b0b0b0;
  cursor: not-allowed;
}
</style>
