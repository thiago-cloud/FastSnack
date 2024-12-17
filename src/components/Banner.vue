<template>
    <div id="main-banner">
      <h1>Faça seu hambúrguer</h1>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Banner',
    components: {}
  };
  </script>
  
  <style scoped>
  #main-banner {
    background-image: url('../../public/img/hamburguer.jpg');
    background-position: center;
    background-size: cover;
    height: 500px;
    background-repeat: no-repeat;
    display: flex;
    align-items: center;
    justify-content: center; /* Mudança para centralizar melhor o texto */
    text-align: center;
    padding: 0 20px; /* Adicionado para evitar que o texto encoste nas bordas em telas menores */
  }
  
  #main-banner h1 {
    color: #fff;
    font-size: 60px;
    padding: 20px 40px;
  }
  
  /* Responsividade */
  @media (max-width: 1024px) {
    #main-banner {
      height: 400px;
    }
  
    #main-banner h1 {
      font-size: 50px;
      padding: 15px 30px;
    }
  }
  
  @media (max-width: 768px) {
    #main-banner {
      height: 300px;
    }
  
    #main-banner h1 {
      font-size: 40px;
      padding: 10px 20px;
    }
  }
  
  @media (max-width: 480px) {
    #main-banner {
      margin-top: 10vh;
      height: 200px;
    }
  
    #main-banner h1 {
      font-size: 30px;
      padding: 5px 15px;
    }
  }
  </style>
  