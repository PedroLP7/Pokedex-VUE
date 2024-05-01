<template>
  <div>
    <Favourites :likedPokes="likedPokes" />
    <Pokedex @likedPokes="updateLikedPokes" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Pokedex from './components/Pokedex.vue';
import Favourites from './components/Favourites.vue';


</script>

<script>
export default {
  components: {
    Pokedex,
    Favourites,
  }, 
  data() {
    return {
      likedPokes: null,
    };
  },
  methods: {
    updateLikedPokes(pokes) {
      this.likedPokes = pokes;
    },
  },
};





</script>
