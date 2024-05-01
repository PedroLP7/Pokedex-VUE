<template >
    <div>
       <h1 class="text-left">MY INVENTORY</h1>

        <div class="container">
            <div class="row ">


        
                
             
                <Item v-for="(item, index) in items1" :key="index" :item="item" />

                <button @click="changeOneItem">Prueba</button>


                <!-- <div v-for="item in items1">
                {{ item.name }}
                 <img :src=" item.sprites.default " alt="">
                  {{ item.quantity }}

                 </div> -->


            </div>

           
        </div>




    
        <Shop />
        



      


        
    </div>
</template>
<script>


import Shop from './Shop.vue'
import axios from 'axios'
import Item from './Item.vue'

export default {
    name: 'Inventory',
    components: {
        Shop,
        Item
        
        },
        methods: {
            changeOneItem() {
      
      const item = this.items1.find(i => i.id === 1);
      if (item) {
        item.quantity += 5;
      }
    },


        getItems() {
              let firstItem =1;
             let lastItem =50
             let desiredItems = [1,2,4,17,23,29,40,46,50,51,77]


            for (let i = firstItem; i <= lastItem; i++) {
                axios.get(`https://pokeapi.co/api/v2/item/${i}`)
                    .then((response) => {
                        if(desiredItems.includes(i)){
                            response.data.quantity = 0
                            this.items1.push(response.data)
                        }
                       


                    })
                    .catch((error) => {
                        console.log(error)
                    })
            }
       


    
            
         }
        
    },

    data() {
        return {
            items1:  []  ,
            
            
        }
    },
    mounted() {
        this.getItems()
        
    }
}
</script>
<style>
    
</style>