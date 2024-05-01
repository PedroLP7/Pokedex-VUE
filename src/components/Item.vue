<template>
    <div class="item">
        <h3>{{ item.name }}</h3>
        <img :src="item.sprites.default" alt="Item image">
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
    /* Agrega estilos si es necesario */
</style>
