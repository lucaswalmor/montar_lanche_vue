<template>
  <NavBar :logo="logo_src" :alt="app_name"></NavBar>
  <router-view/>
  <Footer></Footer>
</template>

<script>
import NavBar from './components/NavBar.vue';
import Footer from './components/Footer.vue';
export default {
    components: { NavBar, Footer },
    data() {
      return {
        logo_src: '/img/logo.png',
        app_name: 'Monte seu lanche'
      }
    }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .main-container {
    min-height: 500px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222; 
  }
</style>