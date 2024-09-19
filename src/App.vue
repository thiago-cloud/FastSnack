<template>
  <div>
    <NavBar :logo="logo_src" :alt="app_name"/>
    <router-view/>
    <Footer/>
  </div>
 
</template>

<script>
import Footer from './components/Footer.vue';
import NavBar from './components/NavBar.vue';

export default{
  name:'App',
  components: {
    NavBar,
    Footer
  },
  data(){
    return{
      logo_src: "/img/logoBurger.png",
      app_name: "Faça seu hamburguer"
    }
  }
}
</script>

<style>

*{
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing:border-box;
}

.main-container{
  margin:50px;
  min-height:350px;

}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom:30px;
  color:#222;
}

</style>
