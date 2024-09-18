<template>
    <div>
        <div>
            <Message :msg="msg" v-show="msg"/>
            <form id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label for="name">Nome do Cliente</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome"/>
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o seu pão: </label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pao</option>
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
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo"/>
                        <span>{{ opcional.tipo }}</span>
                    </div>

                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burger!"/>
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import Message from './Message.vue';

    export default{
        name:'BurgerForm',
        data(){
            return {
                //dados que vem do banco de dados
                paes:null,
                carnes:null,
                opcionaisdata:null,

                //Dados inseridos no formulário pelo cliente
                nome: null,
                pao:null,
                carne:null,
                opcionais:[],
                status:"Solicitado",
                msg:null,

            }
        },
        components: {
            Message,
        },

        methods:{

            //Requisição do backend
            async getIngredientes(){
                const req = await fetch("http://localhost:3000/ingredientes");
                const data = await req.json();

                //Testando a requisição no console
                console.log(data)

                //Recebendo os dados da inserção
                this.paes = data.paes;
                this.carnes = data.carnes;
                this.opcionaisdata = data.opcionais;
                this.msg = data.msg;
            },

            async createBurger(e){
                e.preventDefault();
                
                //Os serão colocados dentro da variavel data via post após o submit
                const data = {
                    name: this.name,
                    pao: this.pao,
                    carne: this.carne,
                    opcionais: Array.from(this.opcionais),
                    status: "Solicitado"
                }

                //Pegando os dados do objeto data convertendo em string e passando para variável dataJson
                const dataJson = JSON.stringify(data)

                //Após pegarmos todos os dados via post agora e só fazer a requisição
                const req = await fetch("http://localhost:3000/burgers",{
                    method: "POST",
                    headers: {"Content-Type": "application/json"},
                    body: dataJson
                })

                const res = await req.json();
                
                //Mostrar mensagem após envio
                this.msg = `Pedido Nº "${res.id}" solicitado com sucesso!`

                //Limpar msg
                setTimeout(()=> {
                    this.msg = ""
                }, 5000)

                //Limpar campos
                this.nome = ""
                this.pao = ""
                this.carne = ""
                this.opcionais = []
            
            }

            
        },
        //Quando o componente for montado faça uma requisição getIngredientes(O mounted e  um 'life Cicle hook')
        mounted(){
                this.getIngredientes();
            }

    }
</script>
<style scoped>
    #burger-form{
        max-width:400px;
        margin:0 auto;
    }

    .input-container{
        display:flex;
        flex-direction:column;
        margin-bottom:20px;
    }
    label{
        font-weight:bold;
        margin-bottom:15px;
        color:#222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select{
        padding: 5px 10px;
        height:40px;
        width: 400px;
        border-radius: 5px;
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title{
        width: 100%;
    }

    .checkbox-container{
        display: flex;
        align-items:flex-start;
        width:33%;
        margin-bottom: 20px;

        transform: scale(1.2); /* Aumenta o tamanho */
        -webkit-transform: scale(1.2); /* Compatibilidade com navegadores WebKit */
        -moz-transform: scale(1.2); /* Compatibilidade com Firefox */
        cursor: pointer; /* Cursor ao passar por cima */
    }

    .checkbox-container span{
        display: block;
        margin-top:12px;
        margin-left:5px;
    }

    .checkbox-container div{
        display: flex;
        align-items: center;
    }

    .checkbox-container span,
    .checkbox-container input{
        width:auto;
    }

    .checkbox-container spam{
        margin-left: 6px;
        font-weight: bold;
    }
    
    .submit-btn{
        background-color:#222;
        color:#fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin:0 auto;
        cursor:pointer;
        transition: .5s;
        border-radius: 5px;
    }

    .submit-btn:hover{
        background-color: transparent;
        color:#222;
    }

    
</style>
