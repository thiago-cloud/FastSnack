<template>
    <div>
      <!-- Header Desktop -->
      <div id="nav" v-if="isDesktop">
        <router-link to="/" id="logo_url">
          <img :src="logo" :alt="alt" id="logo" />
        </router-link>
        <router-link to="/">Home</router-link>
        <router-link to="/pedidos">Pedidos</router-link>
      </div>
  
      <!-- Header Mobile -->
      <div class="head-mobile" v-else>
        <router-link to="/" id="logo_url">
          <img :src="logo" :alt="alt" id="logo" />
        </router-link>
        <button @click="toggleMenu" class="btn-menu" :class="{ ativar: isMenuOpen }">
          <span class="linha"></span>
          <span class="linha"></span>
          <span class="linha"></span>
        </button>
      </div>
  
      <div class="menu-mobile" :class="{ abrir: isMenuOpen }" v-if="!isDesktop">
        <a href="/" @click="closeMenu">Home</a>
        <a href="/pedidos" @click="closeMenu">Pedidos</a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "NavBar",
    props: ["logo", "alt"],
  
    data() {
      return {
        isMenuOpen: false,
        isDesktop: window.innerWidth > 768, // Define o estado inicial com base no tamanho da janela
      };
    },
  
    methods: {
      toggleMenu() {
        this.isMenuOpen = !this.isMenuOpen;
      },
      closeMenu() {
        this.isMenuOpen = false;
      },
      handleResize() {
        this.isDesktop = window.innerWidth > 768; // Atualiza o estado com base no tamanho da tela
      },
    },
  
    mounted() {
      window.addEventListener("resize", this.handleResize); // Escuta o redimensionamento da tela
    },
  
    beforeDestroy() {
      window.removeEventListener("resize", this.handleResize); // Remove o evento ao destruir o componente
    },
  };
  </script>
  
  <style scoped>
  /* Estilo para menu desktop */
  #nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }
  
  #nav #logo_url {
    margin: auto;
    margin-left: 0;
  }
  
  #logo {
    width:70px;
  }
  
  #nav a {
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: 0.5s;
  }
  
  #nav a:hover {
    color: #fff;
  }
  
  /* Estilo para menu mobile */
  .head-mobile {
    width: 100vw;
    height: 10vh;
    position: fixed;
    z-index: 999;
    padding: 20px;
    background-color: #222;
    top: 0;
    border-bottom: 4px solid #111;
  }
  
  img {
    width: 12vw;
  }
  
  .head-mobile .btn-menu {
    width: 12vw;
    height: 6vh;
    border: 2px solid #222;
    cursor: pointer;
    border-radius: 5px;
    background-color: #222;
    position: absolute;
    top: 2vh;
    left: 84vw;
  }
  
  .btn-menu.ativar {
    border: 1px solid #222;
  }
  
  /* Linha do botão */
  .linha {
    width: 80%;
    height: 5px;
    background-color: azure;
    display: block;
    margin: 5px auto;
    border-radius: 5px;
    transition: 0.3s;
  }
  
  .btn-menu.ativar .linha:nth-child(1) {
    transform: translateY(10px) rotate(-45deg);
    background-color: red;
  }
  
  .btn-menu.ativar .linha:nth-child(2) {
    width: 0;
  }
  
  .btn-menu.ativar .linha:nth-child(3) {
    transform: translateY(-10px) rotate(45deg);
    background-color: red;
  }
  
  /* Menu móvel */
  .menu-mobile {
    background-color: #0000008c;
    position: absolute;
    top: 10vh;
    left: 0;
    width: 100%;
    height: 0vh;
    backdrop-filter: blur(10px);
    visibility: hidden;
    overflow: hidden;
    transition: 0.5s;
  }
  
  .menu-mobile a {
    color: azure;
    text-decoration: none;
    display: block;
    padding: 20px 20px;
    font-size: 18pt;
    margin-left: 66vw;
    text-align: end;
  }
  
  .menu-mobile a:hover {
    background-color: #000 !important;
  }
  
  .menu-mobile.abrir {
    visibility: visible;
    height: calc(250vh - 10vh);
    position: fixed;
    z-index: 999;
  }

  @media(max-width:512px){
    #logo {
    width:12vw;
    position: absolute;
    bottom: 1.8vh;
  }
  }
  </style>
  