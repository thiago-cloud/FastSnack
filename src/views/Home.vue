<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Monte seu Burger: </h1>
      <BurgerForm />
    </div>
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import BurgerForm from '@/components/BurgerForm.vue';

export default {
  name: 'Home',
  components: {
    Banner,
    BurgerForm,
  },
};
</script>

<style scoped>
.main-container {
  max-width: 1200px; /* Limita a largura máxima */
  margin: 0 auto; /* Centraliza o conteúdo */
  padding: 20px; /* Espaçamento interno */
  text-align: center; /* Centraliza texto */
}

h1 {
  color: #222;
  font-size: 2rem; /* Tamanho adaptável */
  margin-bottom: 20px;
}

/* Responsividade */
@media (max-width: 768px) {
  .main-container {
    padding: 15px;
  }

  h1 {
    font-size: 1.5rem; /* Reduz tamanho em telas menores */
  }
}

@media (max-width: 480px) {
  .main-container {
    padding: 10px;
   
  }

  h1 {
    font-size: 1.2rem; /* Ajuste para telas muito pequenas */
  }
}
</style>
