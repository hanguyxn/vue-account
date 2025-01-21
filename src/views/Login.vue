<script setup>

import router from '../router.js'
import Loading from '../components/Loading.vue';
import Button from '../components/Button.vue';
import Input from '../components/Input.vue';
import apiClient from '../axios.js';

import { ref } from 'vue';

const username = ref('');
const password = ref('');
const usernameError = ref('');
const passwordError = ref('');
const loading = ref(false);



const login = async () => {
    
  loading.value = true
  const raw = JSON.stringify({
      "username": username.value,
      "password": password.value
  });

  try {
      const response = await apiClient.post("/auth/login", raw)
      console.log(response)
      if (response.status){
          
          console.log(response.data)
          router.push('/profile')
      }{
          if (Array.isArray(response.message)){
              [usernameError.value, passwordError.value, ...value] = result.message
          }else{
              alert(response.data.message)
          }
      }
      
      
  } catch (error) {
    alert("Xay ra loi")
    console.error(error);
  }finally{
    loading.value = false
  }

};

const handleSubmit = () => {
  login()
};

const inputHandle = (value) => {
  username.value = value
  console.log(username.value)
}
const passwordHandle = (value) => {
  password.value = value
  console.log(password.value)
}
</script>

<template>
  <div class="container">
    <div class="card">
      <h1>Form đăng nhập</h1>
      <form @submit.prevent="handleSubmit">
        <Input
            :requiredInput="true"
            @inputEmit="inputHandle"
            :errorMessage="usernameError" 
            label="Tài khoản" 
            placeholder="Nhập tài khoản"
        />
        <Input
            :requiredInput="true"
            @inputEmit="passwordHandle"
            :errorMessage="passwordError" 
            label="Mật khẩu" 
            placeholder="Nhập mật khẩu" 
            type="password" 
        />
        <Button class="btn primary" text="Đăng nhập" type="submit"/>
        <span>Chưa có tài khoản? <strong @click="router.push('register')">Đăng ký</strong></span>
      </form>
      <Loading :active="loading" />
    </div>
  </div>
</template>

<style scoped>

.form .h2{
  font-weight: bold;
  margin-bottom: 20px;
  color: #333;
}


.card {
  border-radius: 8px;
  background-color: rgb(255, 255, 255);
  width: 100%;
  min-width: 400px;
  height: 350px;
  padding: 20px 30px;
  box-shadow: 0 0 5px #ccc;
}
strong:hover{
  color: #5c5c5c;
}

</style>
