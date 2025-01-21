<script setup>
import { ref, defineProps, defineEmits } from 'vue'
const emit = defineEmits(['inputEmit'])

defineProps({
    value: String,
    id: String,
    class: {
        type: String,
        default: "btn",
    },
    type: {
        type: String,
        default: "text",
    },
    placeholder: {
        type: String,
        default: "Enter text",
    },
    label: String,
    errorMessage: String,
    requiredInput: {
        type: Boolean,
        default: false
    }
});

const inputValue = ref('');

const updateValue = () => {
    // console.log(inputValue.value)
    emit('inputEmit', inputValue.value);
}
</script>

<template>
    <div class="form-group">
        <label :for="id" class="form-label"><span class="require">{{ requiredInput ? "*" :"" }}</span>{{ label }}</label>
        <input v-model="inputValue" @blur="updateValue" :id="id" :class="class" :type="type" :placeholder="placeholder" class='form-input' :required="requiredInput"/>
        <span class="form-message">{{ errorMessage }}</span>
    </div>
</template>

<style scoped>

.form-group{
    margin-bottom: 20px;
    text-align: left;
}

label{
    font-size: 14px;
    font-weight: 500px;
    color: #555;
    margin-bottom: 5px;
    display: block;
}
input[type="text"],
input[type="email"],
input[type="password"]{
    width: 100%;
    padding: 10px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 5px;
    outline: none;
    transition: border-color 0.3s ease;
}
input:focus{
    border-color: #007bff;
    box-shadow: 0 0 4px rgba(0, 123, 255, 0.4);
}
.form-group.invalid input {
    border-color: #ff0000;
    box-shadow: 0 0 4px rgba(255, 6, 93, 0.4);
}

.form-message{
    font-size: 12px;
    color: red;
    margin-top: 5px;
    display: block;
}
.require{
    color: red;
}
</style>
