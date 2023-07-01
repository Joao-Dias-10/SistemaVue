<template>
  <div>
 
    <div class="main-container">
      <h5>Faça seu pedido!</h5>
      <BurgerForm />
    </div>
  </div>
</template>

<script>
import BurgerForm from '../components/BurgerForm'

export default {
  name: 'Home',
  components: {
    BurgerForm
  }
}
</script>