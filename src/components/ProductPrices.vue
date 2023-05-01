<template>
  <div class="container">
    <div class="box">
      <b-field grouped>
        <b-field label="Produto" expanded>
          <b-autocomplete
            id="campoProduto"
            field="productName"
            :data="produtoParaBusca"
            icon="magnify"
            placeholder="RTX"
            :open-on-focus=true
            @select="option => selecionarProduto(option)"
            @typing="buscarProdutosAsync">
          <template #empty>Nenhum produto foi encontrado</template>
          </b-autocomplete>
        </b-field>
        <b-field label="Datas" grouped>
          <b-datepicker placeholder="Clique para selecionar" v-model="datas" range></b-datepicker>
          <b-button @click="gerarGrafico" type="is-success" outlined>Gerar Gráfico</b-button>
        </b-field>
      </b-field>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductPrices',
  data () {
    return {
      datas: [],
      produtoIDSelecionado: 0,
      produtoParaBusca: [],
      isLoading: false
    }
  },
  methods: {
    selecionarProduto (option) {
      this.produtoIDSelecionado = option.id
    },
    buscarProdutosAsync (produto) {
      let produtoParaBuscar = produto.trim()
      if (produtoParaBuscar === '') {
        return
      }
      this.produtoParaBusca = []
      this.axios.get('https://localhost:7022/api/Product?name=' + produtoParaBuscar)
        .then(response => {
          response.data.forEach(element => {
            this.produtoParaBusca.push(element)
          })
        })
    },
    gerarGrafico () {
      // Requisição com os dados dos preços

      // Abrir o gráfico em tela
    }
  }
}
</script>

<style scoped>
.container {
  padding-top: 44px;
}

label {
  margin: 6px;
}

.campoProduto {
  display: flex;
  flex-grow: 2;
}

.campoData {
  padding-top: 24px;
}
</style>
