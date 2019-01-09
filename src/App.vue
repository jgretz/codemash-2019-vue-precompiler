<template>
  <div id="app" class="container">
    <Header />
    <Cart />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Cart from './components/Cart.vue'

export default {
  name: 'app',
  components: {
    Header,
    Cart,
  }
}
</script>