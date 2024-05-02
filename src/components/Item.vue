<template>

    <div class="card icard m-3">
        <h3>{{ item.name }}</h3>
        <img  id="itemimg" :src="item.sprites.default" alt="Item image">
        <p>Quantity: {{ item.quantity }}</p>

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
    }
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
</style>
