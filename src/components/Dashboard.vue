<template>
  <div id="burger-table">
    <div>
      <Message :msg="msg" v-show="msg" />
      <div id="burger-table-heading">
        <div class="order-id">#</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.nome }}</div>
        <div>{{ burger.pao }}</div>
        <div>{{ burger.carne }}</div>
        <div>
          <ul>
            <li v-for="(opcional, index) in burger.opcionais" :key="index">
              {{ opcional }}
            </li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updateBurger($event, burger.id)">
            <option value="">Selecione</option>
            <option v-for="statu in status" :key="statu.id" :value="statu.tipo" :selected="burger.status == statu.tipo">
              {{ statu.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "Dashboard",
  components: {
    Message,
  },
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null,
    };
  },

  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();
      this.burgers = data;
      this.getStatus();
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      req.json().then((value) => {
        this.status = value;
      });
    },

    async deleteBurger(id) {
      await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });
      this.msg = `Pedido removido com sucesso!`;
      setTimeout(() => {
        this.msg = "";
      }, 5000);
      this.getPedidos();
    },
    
    async updateBurger(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option });
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });
      const res = await req.json();
      this.msg = `O pedido Nº ${res.id} foi atualizado para o status de ${res.status}`;
      setTimeout(() => {
        this.msg = "";
      }, 5000);
    },
  },
  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #CCC;
}

#burger-table-heading div,
.burger-table-row div {
  width: 19%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  padding: 8px 6px;
  margin-right: 12px;
  margin-bottom:5px;
  border-radius: 5px;
  width: 100%;

}

ul {
  padding-left: 20px;
}

li {
  list-style: disc;
}

.delete-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 8px 10px;
  font-size: 14px;
  cursor: pointer;
  transition: 0.5s;
  border-radius: 5px;
  width:100%;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}

/* Responsividade */
@media (max-width: 768px) {


  #burger-table-heading div,
  .burger-table-row div {
    width: 25%;
  }

  #burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 10%;
  }

}

@media (max-width: 480px) {
  
  #burger-table-heading,
  .burger-table-row {
    flex-direction: column;
  }

  #burger-table-heading div,
  .burger-table-row div {
    width: 100%;
    margin-bottom: 10px;
  }

  #burger-table-heading{
    display:none;
  }

  select {
    width: 100%;
    margin-bottom:10px;
  }

  .delete-btn {
    width: 100%;
    text-align: center;
  }
}
</style>
