<template>
  <div class="container">
    <div class="box">
      <b-field grouped>
        <b-field label="Produto" expanded>
          <b-autocomplete
            id="campoProduto"
            v-model="produtoSelecionado"
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
        <b-field label="Datas">
        <b-datepicker placeholder="Clique para selecionar" v-model="datas" range>
        </b-datepicker>
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
      msg: 'Welcome to Your Vue.js App',
      datas: [],
      produtoSelecionado: '',
      produtoIDSelecionado: 0,
      produtoParaBusca: []
    }
  },
  methods: {
    selecionarProduto (option) {
      this.produtoSelecionado = option.productName
      this.produtoIDSelecionado = option.id
    },
    buscarProdutosAsync () {
      this.produtoParaBusca = []
      this.axios.get('https://localhost:7022/api/Product?name=' + this.produtoSelecionado)
        .then(response => {
          response.data.forEach(element => {
            this.produtoParaBusca.push(element)
          })
        })
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
