<template >
    <div>   
        <h1 v-if="likedPokes" class="text-center">Favourites</h1>
        <h1  v-if="likedPokes&&likedPokes.length==0">No favourites yet , select one </h1>
        <div class="container"id="favourites">
        <div class="row mt-3">
         
            <div class="card col-2 m-5 align-content-center " v-for="pokemon in likedPokes" :key="pokemon.id">
                <svg    class="like mt-3"xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 512 512">
		<path fill="#f44336" d="m47.6 300.4l180.7 168.7c7.5 7 17.4 10.9 27.7 10.9s20.2-3.9 27.7-10.9l180.7-168.7c30.4-28.3 47.6-68 47.6-109.5v-5.8c0-69.9-50.5-129.5-119.4-141c-45.6-7.6-92 7.3-124.6 39.9l-12 12l-12-12c-32.6-32.6-79-47.5-124.6-39.9C50.5 55.6 0 115.2 0 185.1v5.8c0 41.5 17.2 81.2 47.6 109.5" />
	</svg>
              <img :src="pokemon.sprites.front_default" class="card-img-top" alt="...">
              
              <div class="card-body">
                <h5 class="card-title capitalize">{{ pokemon.name }}</h5>
                <p class="card-text">Pokedex Number: {{ pokemon.id }}</p>
                <p class="card-text">Height: {{ pokemon.height }}</p>
                <p class="card-text">Weight: {{ pokemon.weight }}</p>
                <p class="card-text">Types:
                  <span class="capitalize " :style="{ backgroundColor: getColor(type.type.name)}  " v-for="(type, index) in pokemon.types" :key="index">
                    {{ type.type.name }}&nbsp;
                  </span>
                </p>
              </div>
            </div>
          </div>
        </div>
        
    </div>
</template>
<script>
export default {
    props: {
        likedPokes: null,
    },
    data() {
        return {
            
            
        }
    },
    methods: {
        getColor(typeName) {
    switch (typeName) {
        case 'normal':
            return '#A8A77A'; 
        case 'fire':
            return '#EE8130'
        case 'water':
            return '#6390F0'; 
        case 'electric':
            return '#F7D02C'; 
        case 'grass':
            return '#7AC74C'; 
        case 'ice':
            return '#96D9D6'; 
        case 'fighting':
            return '#C22E28'; 
        case 'poison':
            return '#A33EA1'; 
        case 'ground':
            return '#E2BF65'; 
        case 'flying':
            return '#A98FF3'; 
        case 'psychic':
            return '#F95587'; 
        case 'bug':
            return '#A6B91A'; 
        case 'rock':
            return '#B6A136'; 
        case 'ghost':
            return '#735797'; 
        case 'dragon':
            return '#6F35FC'; 
        case 'dark':
            return '#705746';
        case 'steel':
            return '#B7B7CE'; 
        case 'fairy':
            return '#D685AD'; 
        default:
            return '#BDBDBD'; 
    }
},
      
    }
    
}
</script>
<style scoped >
.like{
    cursor: default;
    height: 45px;
    width: 50px;
}

    
</style>