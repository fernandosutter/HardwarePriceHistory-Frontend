<template>
  <div id="app">
    <Header/>
    <ProductPrices/>
    <Footer/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import ProductPrices from './components/ProductPrices'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    ProductPrices,
    Header,
    Footer
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
background-color: rgb(204, 201, 201);
}
</style>
