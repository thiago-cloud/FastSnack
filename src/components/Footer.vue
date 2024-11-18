<template>
    <footer id="footer">
      <p>Faça Seu Hamburguer &copy; 2024</p>
    </footer>
  </template>
  
  <script>
  export default {};
  </script>
  
  <style scoped>
  #footer {
    height: 150px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #fcba03;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
    text-align: center;
    font-size: 16px;
    padding: 10px 20px;
  }
  
  /* Responsividade */
  @media (max-width: 768px) {
    #footer {
      height: auto; /* Ajusta a altura dinamicamente */
      padding: 20px;
      font-size: 14px; /* Reduz o tamanho do texto */
    }
  }
  
  @media (max-width: 480px) {
    #footer {
      font-size: 12px; /* Texto menor em telas muito pequenas */
      padding: 15px;
    }
  }
  
  </style>
  