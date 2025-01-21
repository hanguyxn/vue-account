<script setup>

import { reactive, ref } from 'vue';
import Button from '../components/Button.vue';
import apiClient from '../axios.js';
import Loading from '../components/Loading.vue';
const loading = ref(false);
const profileInfo = reactive({
            "id": 46,
            "created_at": "2025-01-20T01:57:27.079Z",
            "updated_at": "2025-01-20T01:57:27.079Z",
            "deleted_at": null,
            "username": "trinh123",
            "firstname": "ho",
            "lastname": "trinh",
            "role": "user"
        })

const fakeRequest = () => {
    
    try{
        
        // const response = await apiClient.get("/auth/users")
        // console.log(response)
        
    }catch{
        console.log("Khong the fetch ")
    }finally{
        loading.value = false
    }
}
loading.value = true
setTimeout(fakeRequest, 3000)

const uppercase = (str) => (str.charAt(0).toUpperCase() + str.slice(1))
const formatDate = (isoDate) => {
      const date = new Date(isoDate);
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();
      return `${day}/${month}/${year}`;
    }
</script>

<template>
    <Loading :active="loading" />
    <div class="card">
        <h1>Profile</h1>
        <h3>Welcome back {{ `${uppercase(profileInfo.firstname)} ${uppercase(profileInfo.lastname)}`}}</h3>
        <p>Username: {{ profileInfo.username }}</p>
        <p>Create at: {{ formatDate(profileInfo.created_at) }}</p>
        <Button id="profile-btn" text="Edit profile" />
    </div>
    
</template>

<style scoped>


.card {
  border-radius: 8px;
  background-color: rgb(255, 255, 255);
  width: 100%;
  min-width: 95vw;
  height: 90vh;
  padding: 20px 30px;
  box-shadow: 0 0 5px #ccc;
}

p{
    line-height: 2;
}
#profile-btn{
    width: 200px;
}
</style>