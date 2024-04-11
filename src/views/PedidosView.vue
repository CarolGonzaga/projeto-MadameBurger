<template>
  <div class="main-container">
    <h1>Gerenciar pedidos:</h1>
    <Dashboard />
  </div>
</template>

<script>
  import Dashboard from '../components/Dashboard.vue'
  
  export default {
    name: 'PedidosView',

    components: { 
      Dashboard 
    },
  }
  
</script>

<style scoped>

  h1 {
  font-size: 40px;
  color: #B82E29;
  text-transform: uppercase;
  text-align: center;
  margin: 30px 0;
}

</style>