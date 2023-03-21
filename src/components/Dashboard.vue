<template>
  <div id="pedido_id-table" v-if="pedidos">
    <div>
      <div id="pedido_id-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Tipo:</div>
        <div>Categoria:</div>
        <div>Opções:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="pedido_id-table-rows">
      <div class="pedido_id-table-row" v-for="pedido_id in pedidos" :key="pedido_id.id">
        <div class="order-number">{{ pedido_id.id }}</div>
        <div>{{ pedido_id.nome }}</div>
        <div>{{ pedido_id.campo1 }}</div>
        <div>{{ pedido_id.campo2 }}</div>
        <div>
          <ul v-for="(opcional, index) in pedido_id.opcionais" :key="index">
            <li>{{ opcional }}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updatePedido($event, pedido_id.id)">
            <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="pedido_id.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deletePedido(pedido_id.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="text-primary">
    <h2 class="text-danger h5">Não há pedidos no momento!</h2>
  </div>
</template>
<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        pedidos: null,
        pedido_id: null,
        status: []
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch('https://my-json-server.typicode.com/RubenFontes/json-server-api/pedidos')

        const data = await req.json()

        this.pedidos = data

        // Resgata os status de pedidos
        this.getStatus()

      },
      async getStatus() {

        const req = await fetch('https://my-json-server.typicode.com/RubenFontes/json-server-api/status')

        const data = await req.json()

        this.status = data

      },
      async deletePedido(id) {

        const req = await fetch(`https://my-json-server.typicode.com/RubenFontes/json-server-api/pedidos/${id}`, {
          method: "DELETE"
        });

        const res = await req.json()

        this.getPedidos()

      },
      async updatePedido(event, id) {

        const option = event.target.value;

        const dataJson = JSON.stringify({status: option});

        const req = await fetch(`https://my-json-server.typicode.com/RubenFontes/json-server-api/pedidos/${id}`, {
          method: "PATCH",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });

        const res = await req.json()

        console.log(res)

      }
    },
    mounted () {
    this.getPedidos()
    }
  }

  /** 
    Public API
    https://my-json-server.typicode.com/RubenFontes/json-server-api
  
    Environment Development API
    http://localhost:3000
  **/

</script>

<style scoped>
  #pedido_id-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #pedido_id-table-heading,
  #pedido_id-table-rows,
  .pedido_id-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #pedido_id-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .pedido_id-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #pedido_id-table-heading div,
  .pedido_id-table-row div {
    width: 19%;
  }

  #pedido_id-table-heading .order-id,
  .pedido_id-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 3px 5px;
    margin-right: 5px;
    max-width: 100px;
  }

  .delete-btn {
    background-color: #6574cd;
    font-weight: bold;
    padding: 5px 10px;
    font-size: .8rem;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    border: none;
    border-radius: 2px;
    color: white;
  }
  
  .delete-btn:hover {
    filter: brightness(0.9);
  }

</style>