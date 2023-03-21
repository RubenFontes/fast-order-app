<template>
  <Message :msg="msg" v-show="msg" />
  <div>
    <form id="pedido-form" method="POST" @submit="createPedido">
      <div class="input-container">
        <label for="nome">Nome:</label>
        <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
      </div>
      <div class="input-container">
        <label for="campo1">Selecione um tipo:</label>
        <select name="campo1" id="campo1" v-model="campo1">
          <option value="">Tipo 1</option>
          <option v-for="campo1 in tipos" :key="campo1.id" :value="campo1.tipo">{{ campo1.tipo }}</option>
        </select>
      </div>
      <div class="input-container">
        <label for="campo2">Escolha uma categoria:</label>
        <select name="campo2" id="campo2" v-model="campo2">
          <option value="">Categoria 1</option>
          <option v-for="campo2 in categorias" :key="campo2.id" :value="campo2.tipo">{{ campo2.tipo }}</option>
        </select>
      </div>
      <div id="opcionais-container" class="input-container">
        <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
        <div class="checkbox-container h6" v-for="opcional in opcionaisdata" :key="opcional.id">
          <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
          <span>{{ opcional.tipo }}</span>
        </div>
      </div>
      <div class="input-container">
        <input class="submit-btn" type="submit" value="Enviar solicitação!">
      </div>
    </form>
  </div>
</template>

<script>
import Message from './Message'

export default {
  name: "Form",
  data() {
    return {
      tipos: null,
      categorias: null,
      opcionaisdata: null,
      nome: null,
      campo1: null,
      campo2: null,
      opcionais: [],
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async getData() {
      const req = await fetch('https://my-json-server.typicode.com/RubenFontes/json-server-api/data')
      const data = await req.json()

      this.tipos = data.tipos
      this.categorias = data.categorias
      this.opcionaisdata = data.opcionais
    },
    async createPedido(e) {

      e.preventDefault()

      const data = {
        nome: this.nome,
        campo2: this.campo2,
        campo1: this.campo1,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)    

      const req = await fetch("https://my-json-server.typicode.com/RubenFontes/json-server-api/pedidos", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });

      const res = await req.json()

      console.log(res)

      this.msg = "Pedido realizado com sucesso!"

      // clear message
      setTimeout(() => this.msg = "", 3000)

      // limpar campos
      this.nome = ""
      this.campo2 = ""
      this.campo1 = ""
      this.opcionais = []
      
    }
  },
  mounted () {
    this.getData()
  },
  components: {
    Message
  }
}
</script>

<style scoped>
  #pedido-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: 500;
    margin-bottom: 15px;
    color: #222;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
    border: 1px solid #6574cd;
    border-radius: 4px;
  }

  #opcionais-container {
    width: 300px;
    display: flex;
    text-align: center;
    flex-direction: row;
    flex-wrap: wrap;
  }

  #opcionais-title {
    width: 100%;
  }

  .checkbox-container {
    font-size: .8rem;
    display: flex;
    justify-content: center;
    width: 33%;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
  }

  .submit-btn {
    background-color: #6574CD;
    border: none;
    border-radius: 4px;
    color:white;
    font-weight: bold;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: #5661B3;
  }
</style>