<template>
    <div class="message-container">
      <p>{{ msg }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Message',
    props: {
      msg: String,
    },
  };
  </script>
  
  <style scoped>
  .message-container {
    color: #004085;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
    text-align: center;
    font-size: 16px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  /* Responsividade */
  @media (max-width: 768px) {
    .message-container {
      max-width: 90%; /* Adapta a largura para telas médias */
      font-size: 14px; /* Reduz o tamanho do texto */
      padding: 8px; /* Menor espaçamento interno */
    }
  }
  
  @media (max-width: 480px) {
    .message-container {
      max-width: 95%; /* Quase a largura total da tela */
      font-size: 12px; /* Texto ainda menor para telas pequenas */
      margin: 20px auto;
      padding: 6px;
    }
  }
  </style>
  