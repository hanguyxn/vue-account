<script setup>
import { ref } from 'vue';
import router from '../router.js';
import apiClient from '../axios.js';
import Button from '../components/Button.vue';
import Input from '../components/Input.vue';
import Loading from '../components/Loading.vue';
// Biến trạng thái
const username = ref('');
const password = ref('');
const firstName = ref('');
const lastName = ref('');
const confirmPassword = ref('');
const usernameError = ref('');
const passwordError = ref('');
const confirmPasswordError = ref('');
const loading = ref(false);

// Hàm xử lý đăng ký
const register = async () => {
  loading.value = true
  if (password.value !== confirmPassword.value) {
        confirmPasswordError.value = 'Passwords do not match';
        return;
      }
  const raw = JSON.stringify({
    username: username.value,
    password: password.value,
    firstname: firstName.value,
    lastname: lastName.value,
  });
  try {
    const response = await apiClient.post("/auth/register", raw);
    if (response.status === 201 || response.message === "User created successfully") {
      router.push('/login');
    } else {
      console.log(result);
    }
  } catch (error) {
    alert("Xay ra loi")
    console.error(error);
  }finally{
    loading.value = false
  }
};

// Hàm xử lý form submit
const handleSubmit = () => {
  register()
};

// Các hàm xử lý input
const inputHandle = (value) => {
  username.value = value;
};

const passwordHandle = (value) => {
  password.value = value;
};

const confirmPasswordHandle = (value) => {
  confirmPassword.value = value;
};

const firstNameHandle = (value) => {
  firstName.value = value;
};

const lastNameHandle = (value) => {
  lastName.value = value;
};
</script>

<template>
    <div class="container">
      <div class="card">
        <h1>Form đăng ký</h1>
        <form @submit.prevent="handleSubmit">
          <Input
            @inputEmit="firstNameHandle"
            label="Tên" 
            placeholder="Nhập tên"
          />
          <Input 
            @inputEmit="lastNameHandle"
            label="Họ" 
            placeholder="Nhập họ"
          />
          <Input 
            :requiredInput="true"
            @inputEmit="inputHandle"
            :errorMessage="usernameError" 
            label="Tài khoản" 
            placeholder="Nhập tên đăng nhập"
          />
          <Input
            :requiredInput="true"
            @inputEmit="passwordHandle"
            :errorMessage="passwordError" 
            label="Mật khẩu" 
            placeholder="Nhập mật khẩu của bạn" 
            type="password" 
          />
          <Input 
            :requiredInput="true"
            @inputEmit="confirmPasswordHandle"
            :errorMessage="confirmPasswordError" 
            label="Nhập lại mật khẩu" 
            placeholder="Nhập lại mật khẩu" 
            type="password" 
          />
          <Button class="btn primary" text="Đăng ký" type="submit"/>
          <span>Bạn đã có tài khoản? <strong @click="router.push('/login')">Đăng nhập</strong></span>
        </form>
        <Loading :active="loading" />
      </div>
    </div>
  </template>
  
<style scoped>
.card {
  border-radius: 8px;
  background-color: rgb(255, 255, 255);
  width: 100%;
  min-width: 400px;
  height: 600px;
  padding: 20px 30px;
  box-shadow: 0 0 5px #ccc;
}
strong:hover{
  color: #5c5c5c;
}

</style>
