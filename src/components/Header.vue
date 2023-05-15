<template>
  <header class="header">
    <h1 class="header-text">HardwarePriceHistory</h1>
  </header>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style scoped>
.header {
  /* Alinhar texto para o inicio */
  text-align: start;
  /* Cor de fundo */
  background-color: #333;
  /* Cor do texto */
  color: white;
  /* Fixar o cabeçalho na parte superior */
  position: fixed;
  /* Colocar o cabeçalho no topo da página */
  top: 0;
  /* Alinhar o cabeçalho à esquerda */
  left: 0;
  /* Definir a largura máxima do cabeçalho */
  width: 100%;
  z-index: 1;
}

.header-text {
  color: white;
  margin: 10px;
  font-size: 16px;
}</style>
