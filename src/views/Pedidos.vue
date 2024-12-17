<template>
  <div class="main-container">
    <h1>Pedidos</h1>
    <Dashboard />
  </div>
</template>

<script>
import Dashboard from '@/components/Dashboard.vue';

export default {
  name: 'Pedidos',
  components: {
    Dashboard,
  },
};
</script>

<style scoped>
  .main-container {
    max-width: 1200px; /* Define a largura máxima */
    margin: 0 auto; /* Centraliza horizontalmente */
    padding: 20px; /* Espaçamento interno */
    text-align: center; /* Centraliza texto */
  }

  h1 {
    font-size: 2rem; /* Tamanho inicial do título */
    color: #222;
    margin-bottom: 20px;
  }

  /* Responsividade */
  @media (max-width: 768px) {
    .main-container {
      padding: 15px;
    }

    h1 {
      font-size: 1.5rem; /* Reduz tamanho do título em telas menores */
    }
  }

@media (max-width: 480px) {
  .main-container {
    padding: 10px;
    margin-top:13vh;
  }

  h1 {
    font-size: 1.2rem; /* Ajuste para telas muito pequenas */
  }
}

</style>
