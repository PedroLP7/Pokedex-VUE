<template>

    <div class="card icard m-3 align-items-center" v-bind:class="{'Max' : item.quantity===item.maxQuantity} ">
        <h3>{{ item.name.replace("-"," ") }}</h3>
        <img  id="itemimg" class="" :src="item.sprites.default" alt="Item image">
        <!-- <p>Quantity: {{ item.quantity }}</p> -->
        <!-- <div v-if="item.quantity==item.maxQuantity"> ESTA AL MAXIMO</div> -->
        <p class="text-center">{{ item.quantity }}/{{ item.maxQuantity }}</p>

    </div>

   
</template>

<script>
export default {
    name: 'Item',
    props: {
        item: {
            type: Object,
            required: true
        }
        
    }, data() {
        return {
           
            
            
        }
    },
   
}
</script>

<style>
    #itemimg{
        width:50px;
        height: 50px;
    }

    .icard{
       
        width: 180px;
    }
    .Max{
        background-color: red;
    }
</style>
