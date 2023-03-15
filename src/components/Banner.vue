<template>
  <div id="main-banner">
    <h1 class="h1">Pedido Expresso</h1>
    <p class="display-4">Um Web App Open Source feito com Node.js e Vue.js</p>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>

  #main-banner {
    margin: 85px 0;
    padding: 0 20px;
    background-color: #E6E8FF;
    height: 45vh;
    display: flex;
    flex-direction: column;
    text-align: center;
    justify-content: center;
  }

  #main-banner h1 {
    font-size: 2.5rem;
  }

  #main-banner p{
    font-size: 1.5rem;
    font-weight: 400;
    color: #2f365f;
  }

</style>