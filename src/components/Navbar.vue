<template>
  <div>
    <div id="nav">
      <router-link id="logo-url" to="/">
        <img id="logo" :src="logo" :alt="alt">
      </router-link>
      <router-link to="/#main-container">Realizar Pedido</router-link>
      <!--<a href="/#main-container">Fazer Pedido</a>-->
      <router-link to="/pedidos">Pedidos</router-link>
    </div>
  </div>
</template>

<script>

export default {
  name: "Navbar",
  props: ["logo", "alt"]
}

</script>

<style scoped>
  #nav {
    position: fixed;
    top: 0;
    min-width: 100vw;
    height: 85px;
    background-color: white;
    padding: 0 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    border-bottom: 1px solid rgb(230, 230, 230);
  }

  #nav #logo-url {
    margin: auto;
    margin-left: 0;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #nav a {
    color: black;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }

  #nav a:hover {
    color: #FFF;
  }
</style>