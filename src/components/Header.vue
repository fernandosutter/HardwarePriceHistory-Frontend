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

.header{
  text-align: start; /* Alinhar texto para o inicio */
  background-color: #333; /* Cor de fundo */
  color: white; /* Cor do texto */
  position: fixed; /* Fixar o cabeçalho na parte superior */
  top: 0; /* Colocar o cabeçalho no topo da página */
  left: 0; /* Alinhar o cabeçalho à esquerda */
  width: 100%; /* Definir a largura máxima do cabeçalho */
}

.header-text{
  color: white;
  margin: 10px;
}

</style>
