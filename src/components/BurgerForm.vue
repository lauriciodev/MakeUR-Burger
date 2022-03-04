<template>
<div>
    
    <div> 
        <form id="burg__form"  @submit="createBurger($event)">
         <div class="input__container">
            <label for="nome">Nome</label>
            <input type="text" id="nome" v-model="nome" placeholder="Digite o seu nome">
         </div>
         <div class="input__container">
            <label for="pao">Escolha o pão:</label>
            <select name="pao" id="pao" v-model="pao">
                <option value=""> Selecione o seu pão</option>
                <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                    {{ pao.tipo }}</option>
            </select>
         </div>
          <div class="input__container">
            <label for="carne">Escolha a carne do seu burguer:</label>
            <select name="carne" id="carne" v-model="carne">
                <option value=""> Selecione o sua carne</option>
                  <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
                    {{ carne.tipo }}</option>
            </select>
         </div>
          <div id="opcionais__container" class="input__container">
            <label id="opcionais__title" for="opicionais">Selecione os opcionais:</label>
            <div class="chk_container" v-for="opcional in opcionaisdata" :key="opcional.id">
          <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
            <span>{{ opcional.tipo }}</span>
         </div>
           </div>
         <div class="input__container">
             <input type="submit" class="submit__btn" value="Criar Meu Burger">
         </div>
        </form>
    </div>
    <Msg :msg="msg" v-show="msg"/>
</div>
</template>
<script>
import Msg from "./Msg.vue"


export default{
    name: "BurgerForm",
    components:{
         Msg
    },
    data(){
        return{
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao:null,
            carne: null,
            opcionais: [],
            msg: null
        }
    },

     methods: {
    async getIngredientes() {
      const req = await fetch('http://localhost:3000/ingredientes')
      const data = await req.json()
      
      //pegando da api e atribuindo a variavel

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;

    },
    async createBurger(e){
        e.preventDefault();
      
      const data = {
          nome: this.nome,
          carne: this.carne,
          pao: this.pao,
          opcionais: Array.from(this.opcionais),
          status: "Solicitado"
      }
      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
          method: "POST",
          headers: {
              "Content-type": "application/json"
          },
          body: dataJson
      });
      const res = await req.json();
      //colocar mensagem no sistema

      this.msg = ` Pedido Nº ${res.id} Resalizado com Sucesso !!`;

      setTimeout(() => this.msg = null ,5000)

      //limpar campos
      this.nome = "";
      this.carne = "";
      this.pao = "";
      this.opcionais = this.opcionais;

      
    

    }
    },
    mounted () {
    this.getIngredientes()
  }
}
</script>
<style scoped>
#burg__form{
    max-width: 500px;
    margin: 0 auto;
    background-color: rgb(0, 0, 0);
    padding: 20px;
    box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.63);
   
}

.input__container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
    gap: 10px;
}

.input__container label{
    color: rgb(255, 196, 0);
    font-size: 1.2rem;
    padding: 5px 10px;
    border-left:4px solid white;
}

input,select{
    padding: 5px 10px;
    width: 100%;
    font-size: 1.2rem;
}
#opcionais__container{
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais__container label{
    width: 100%;
}

#span__check{
    color: rgb(255, 217, 0);
}

.chk_container{
    display: flex;
    width: 100px;
    margin-bottom: 20px;

}


.chk__container span,
.chk__container input{
    border:none;
    
}

.chk_container input{
width: 15px;
height: 15px;
}

.chk_container label{
    border: none;
}

.chk_container span{
    margin-left: 6px;
    color: rgb(255, 217, 0);
}

.submit__btn{
   background-color: rgb(255, 187, 0); 
   border: 1px solid white;
   color: rgb(255, 255, 255);
   text-transform: uppercase;
   font-weight: 600;
    transition: .3s;
    font-size: 1.2rem;
}

.submit__btn:hover{
    background-color: rgb(255, 208, 0);
    color: black;
}



</style>
