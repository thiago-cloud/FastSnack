<template>
    <div>
      <div>
        <Message :msg="msg" v-show="msg" />
        <form id="burger-form" @submit="createBurger">
          <div class="input-container">
            <label for="name">Nome do Cliente</label>
            <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome" />
          </div>
          <div class="input-container">
            <label for="pao">Escolha o seu pão:</label>
            <select name="pao" id="pao" v-model="pao">
              <option value="">Selecione o seu pão</option>
              <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
            </select>
          </div>
          <div class="input-container">
            <label for="carne">Escolha a carne do seu Burger:</label>
            <select name="carne" id="carne" v-model="carne">
              <option value="">Selecione o tipo de carne</option>
              <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
            </select>
          </div>
          <div id="opcionais-container" class="input-container">
            <label for="opcionais" id="opcionais-title">Selecione os opcionais:</label>
            <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
              <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo" />
              <span>{{ opcional.tipo }}</span>
            </div>
          </div>
          <div class="input-container">
            <input type="submit" class="submit-btn" value="Criar meu Burger!" />
          </div>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import Message from "./Message.vue";
  
  export default {
    name: "BurgerForm",
    data() {
      return {
        paes: null,
        carnes: null,
        opcionaisdata: null,
        nome: null,
        pao: null,
        carne: null,
        opcionais: [],
        status: "Solicitado",
        msg: null,
      };
    },
    components: {
      Message,
    },
    methods: {
      async getIngredientes() {
        const req = await fetch("http://localhost:3000/ingredientes");
        const data = await req.json();
        this.paes = data.paes;
        this.carnes = data.carnes;
        this.opcionaisdata = data.opcionais;
        this.msg = data.msg;
      },
      async createBurger(e) {
        e.preventDefault();
        const data = {
          name: this.name,
          pao: this.pao,
          carne: this.carne,
          opcionais: Array.from(this.opcionais),
          status: "Solicitado",
        };
        const dataJson = JSON.stringify(data);
        const req = await fetch("http://localhost:3000/burgers", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: dataJson,
        });
        const res = await req.json();
        this.msg = `Pedido Nº "${res.id}" solicitado com sucesso!`;
        setTimeout(() => {
          this.msg = "";
        }, 5000);
        this.nome = "";
        this.pao = "";
        this.carne = "";
        this.opcionais = [];
      },
    },
    mounted() {
      this.getIngredientes();
    },
  };
  </script>
  
  <style scoped>
  #burger-form {
    max-width: 100%;
    width: 400px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  
  label {
    font-weight: bold;
    margin-bottom: 10px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
    width: 100%;
  }
  
  input,
  select {
    padding: 10px;
    height: 40px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  
  #opcionais-container {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    gap: 10px;
  }
  
  .checkbox-container {
    display: flex;
    align-items: center;
    width: calc(33.33% - 10px);
  }
  
  .checkbox-container span {
    margin-left: 5px;
    font-size: 14px;
  }
  
  .submit-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.5s;
    height:40px;
  }
  
  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
  
  /* Responsividade */
  @media (max-width: 768px) {
    #burger-form {
      width: 100%;
      padding: 10px;
    }

    input,
    select {
    height: 20px;
    
  }
  
    .checkbox-container {
      width: calc(50% - 10px);
    }
  }
  
  @media (max-width: 480px) {
    .checkbox-container {
      width: 100%;
    }
  
    input,
    select {
      height: 40px;
    }
  }
  </style>
  