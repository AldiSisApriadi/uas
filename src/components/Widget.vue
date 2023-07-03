<template>
    <div class="custom-widget">
      <h2>{{ customTitle }}</h2>
      <p>{{ customMessage }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        customTitle: 'Custom Widget Title',
        customMessage: 'Greetings! This is a custom widget.',
      };
    },
  };
  </script>
  
  <style scoped>
  .custom-widget {
    border: 1px solid #440ae4;
    padding: 20px;
    margin-bottom: 20px;
  }
  </style>
  