<template>
    <div v-if="active" class="fullscreen-loader">
      <div class="spinner"></div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  defineProps({
    active: {
        type: Boolean,
        required: true
    },
    isFullScreen: {
        type: Boolean,
        default: true
    }
  })
  </script>
  
  <style scoped>
  .fullscreen-loader {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
  }
  .spinner {
    border: 4px solid #f3f3f3;
    border-top: 4px solid #3498db;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    animation: spin 1s linear infinite;
  }
  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  </style>
  