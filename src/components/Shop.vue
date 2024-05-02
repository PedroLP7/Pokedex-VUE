<template >
    <div>

        <h1 class="text-center"> Shop</h1>


<div class="container">
    <div class="row">

        <div class="card card-blue m-3" v-for="(item,index) in shopItems" :key="index">
            <h3>{{ item.name }}</h3>
        <img  id="itemimg" :src="item.sprites.default" alt="Item image">
        <p>Quantity: {{ item.quantity }}</p>
        <button class="btn  btn-primary "@click="desiredPlus(item)">+</button> <p class="mt-2">{{ item.desiredQuantity}}</p> <button  @click="desiredLess(item)" class="btn btn-danger">-</button>
        </div>


        <button class="btn btn-warning" @click="BuyItems()">Comprar</button>
        
    
       



    </div>





</div>
        
        
    </div>
</template>
<script>
import axios from 'axios'
export default {
    name : 'Shop',
    emits: ['buy'],

    data() {
        return {
            shopItems: [],
            
            
            
           
            
        }
    },
    methods: {
        getItems() {
              let firstItem =1;
             let lastItem =50
             let desiredItems = [1,2,4,17,23,29,40,46,50,51,77]


            for (let i = firstItem; i <= lastItem; i++) {
                axios.get(`https://pokeapi.co/api/v2/item/${i}`)
                    .then((response) => {
                        if(desiredItems.includes(i)){
                            response.data.quantity = 50
                            response.data.desiredQuantity = 0
                            this.shopItems.push(response.data)
                        }
                       


                    })
                    .catch((error) => {
                        console.log(error)
                    })
            }
        },
        desiredPlus(item){
           item.desiredQuantity++

            
        },
        desiredLess(item){
            if(item.desiredQuantity > 0){
                item.desiredQuantity--
            }
            
        
    
        },
        BuyItems(){
            this.shopItems.forEach(item => {
                item.quantity -= item.desiredQuantity
                this.$emit('buy', { id: item.id, desiredQuantity: item.desiredQuantity }); 
                console.log( 'id '+item.id +' quantity  ' +item.desiredQuantity)
                item.desiredQuantity = 0
                
                
              
               
                
            })
           
        }
        
    },

    created() {
        this.getItems()
    }
    
}
</script>
<style >

.card-blue{
    align-items: center;
    height: 280px;
  
    width: 250px;

}

.button1{
    background: #FF943A;
}
.button2{
    background: #B53AF7;
}
    
</style>