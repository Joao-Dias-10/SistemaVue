<template>
  <div>
    <div class="main-container">
      <h5>Gerenciar pedidos:</h5>
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