<template>
  <div>
    <div class="main-container">
      <h1>Gerenciar pedidos:</h1>
      <Dashboard />
    </div>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard'

export default {
  name: 'Pedidos',
  components: {
    Dashboard
  }
}
</script>

<style scoped>
  .main-container{
    margin: 85px 0;
    padding: 100px 0;
  }
</style>