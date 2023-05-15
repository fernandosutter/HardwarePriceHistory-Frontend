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
    <div class="chart">
      <GChart
        type="LineChart"
        :data="dadosGrafico"
        :options="chartOptions"
        :resizeDebounce="500"
      />
    </div>
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts/legacy'

export default {
  components: { GChart },
  name: 'ProductPrices',
  data () {
    return {
      datas: [],
      produtoIDSelecionado: 0,
      produtoParaBusca: [],
      isLoading: false,
      colunasGrafico: ['Data', 'Preço'],
      dadosGrafico: [this.colunasGrafico],
      chartOptions: {
        title: 'Preço do produto',
        legend: { position: 'bottom' },
        hAxis: {
          title: 'Data'
        },
        vAxis: {
          title: 'Preço'
        },
        height: 600
      }
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
      this.dadosGrafico = []
      this.dadosGrafico.push(this.colunasGrafico)
      this.axios.get('https://localhost:7022/api/ProductPrice?productId=' + this.produtoIDSelecionado + '&startDate=' + this.datas[0] + '&endDate=' + this.datas[1])
        .then(response => {
          response.data.forEach(element => {
            this.dadosGrafico.push([element.date, element.price])
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

.chart{
  margin-bottom: 104px;
}
</style>
