<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>
<script>
import Navbar from './components/Navbar'
import Footer from './components/Footer'

export default {
  data: function() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Pulcher Code - desafio"
    }
  },
  components: {
    Navbar,
    Footer
  }
}
</script>

<style>

  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  html{
    scroll-behavior: smooth;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  .main-container h1{
    font-weight: 100;
  }

  .main-container h2{
    text-align: center;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
