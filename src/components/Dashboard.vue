<template>
<Msg :msg="msg" v-show="msg"/>
 <div id="burger__table">
    <div>
        <div id="burger__table__heading">
          <div class="order__id">#</div>
          <div>Cliente:</div>
          <div>Pão</div>
          <div>Carne</div>
          <div>Opcionais</div>
          <div>Ações</div>
        </div>
    </div>
   <div id="burger__table__rows">
       <div class="burger__table__row" v-for="burger in burgers" :key="burger.id">
        <div class="order__number">{{ burger.id }}</div>
        <div>{{ burger.nome }} </div>
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
            <select name="status" class="status" @change="updateBurger($event, burger.id)" >
                <option value="">Selecione</option>
                <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">
                    {{ s.tipo }}
                </option>
            </select>
            <button class="delete__btn" @click="deleteBurger(burger.id)">cancelar</button>
        </div>
     </div>
     

   </div>
  </div>
</template>
<script>
import Msg from "./Msg.vue"

export default{
    name: "Dashboard",

    data(){
        return{
           burgers: null,
           burger_id: null,
           status: [],
           msg: null
        }
    },
    components:{
        Msg
    },
    methods:{
        async getPedidos(){
            const req = await fetch("http://localhost:3000/burgers");

            const data = await req.json();

            this.burgers = data;



            //resgatar os status
            this.getStatus();



        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;

        },

        async deleteBurger(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`,
            {method: "DELETE"}
            );

            const res = await req.json();

              //colocar mensagem no sistema

              this.msg = ` Pedido Cancelado Com Sucesso !!`;

                setTimeout(() => this.msg = null ,2000)



            //msg
            this.getPedidos();


        },

        async updateBurger(event, id){
            const option = event.target.value;
            const dataJson = JSON.stringify({ status: option});

            const req = await fetch(`http://localhost:3000/burgers/${id}`,
            {
                method: "PATCH",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            }
            );
            const res = await req.json();

             //colocar mensagem no sistema

              this.msg = ` O Pedido ${res.id} Foi Atualizado Para ${res.status} `;

                setTimeout(() => this.msg = null ,2000)

             

        }

    },
    mounted(){
        this.getPedidos();

    }





}
</script>
<style scoped>
#burger__table{
    max-width: 1200px;
    margin: 0 auto;
}

.burger__table__row{
    font-size: 1.2rem;
    font-weight: 600;

}



#burger__table__heading,
#burger__table__rows,
.burger__table__row {
    display: flex;
    flex-wrap: wrap;

    }

#burger__table__heading{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid rgb(255, 208, 0);
}

#burger__table__heading div,
.burger__table__row div{
    width: 19%;
}

.burger__table__row{
   width: 100%;
   padding: 12px;
   border-bottom: 1px solid rgba(56, 56, 56, 0.705); 
}

#burger__table__heading .order__id,
.burger__table__row .order__number{
    width: 5%;
}

select{
    margin-right: 12px;
    padding:10px 6px;
    font-size: .8rem;
}

.delete__btn{
    background-color: rgb(255, 174, 0);
    color: white;
    font-weight: bold;
    border: 2px solid white;
    padding:10px ;
    font-size: 16px;
    margin:  0 auto;
    cursor: pointer;
    transition: .3s;

}

.delete__btn:hover{
    background-color: rgb(255, 136, 0);
    color: white;
    font-weight: bold;
    border: 2px solid rgb(0, 0, 0);
   

}




</style>
