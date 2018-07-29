<template>
  <div>
    <h1>{{ msg }}</h1>
    <div>
      <router-link tag="li" to="/">
        <a>/Home</a>
      </router-link>
      <div class="div-margin-top">
        <input type="text" v-model="txtZip"/>
        <button type="button" v-on:click="find">Pesquisar</button>
      </div>
      <div v-if="zipCode" class="div-margin-top">
        <div v-if="zipCode.cep">
          {{zipCode.cep}}
        </div>
        <div v-if="zipCode.logradouro">
          {{zipCode.logradouro}}
        </div>
        <div v-if="zipCode.complemento">
          {{zipCode.complemento}}
        </div>
        <div v-if="zipCode.bairro">
          {{zipCode.bairro}}
        </div>
        <div v-if="zipCode.localidade">
          {{zipCode.localidade}} / {{zipCode.uf}}
        </div>
        <div v-if="zipCode.unidade">
          {{zipCode.unidade}}
        </div>
        <div v-if="zipCode.ibge">
          {{zipCode.ibge}}
        </div>
        <div v-if="zipCode.gia">
          {{zipCode.gia}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ZipCode',
  data () {
    return {
      msg: 'Pagina de Pesquisa CEP do Brasil',
      txtZip: '',
      zipCode: null
    }
  },
  methods: {
    find: function (e) {
      var t = this
      if (!this.txtZip || this.txtZip.length < 8) {
        alert('Digite o cep corretamente')
      } else {
        this.$http.get('http://viacep.com.br/ws/{0}/json/'.replace('{0}', this.txtZip))
          .then(response => {
            t.zipCode = response.body
            console.log(t.zipCode)
          })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.div-margin-top {
  margin-top: 10px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
