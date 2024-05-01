<template>
    <div>
      <h1 class="text-center">Pokedex</h1>
  
      <div class="container"id="pokedex">
        <div class="row mt-3">
            hola
         
            <div class="card col-3 m-5 align-content-center " v-for="pokemon in pokemons" :key="pokemon.id">
                <svg  @click="getLike(pokemon)"  class="like mt-3"xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 512 512">
		<path fill="#e0cccc" d="m47.6 300.4l180.7 168.7c7.5 7 17.4 10.9 27.7 10.9s20.2-3.9 27.7-10.9l180.7-168.7c30.4-28.3 47.6-68 47.6-109.5v-5.8c0-69.9-50.5-129.5-119.4-141c-45.6-7.6-92 7.3-124.6 39.9l-12 12l-12-12c-32.6-32.6-79-47.5-124.6-39.9C50.5 55.6 0 115.2 0 185.1v5.8c0 41.5 17.2 81.2 47.6 109.5" />
	</svg>
              <img :src="pokemon.sprites.front_default" class="card-img-top" alt="...">
              
              <div class="card-body">
                <h5 class="card-title capitalize">{{ pokemon.name }}</h5>
                <p class="card-text">Pokedex Number: {{ pokemon.id }}</p>
                <p class="card-text">Height: {{ pokemon.height }}</p>
                <p class="card-text">Weight: {{ pokemon.weight }}</p>
                <p class="card-text">Types:
                  <span class="capitalize" :style="{ backgroundColor: getColor(type.type.name)}  " v-for="(type, index) in pokemon.types" :key="index">
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
import axios from 'axios'
export default {

    data() {
        return {
            pokemons: []
            ,
            likedPokes: []
            
        }
    },
    methods: {

        getPokemons() {
            const me = this;

            const lastPoke = 151;
            const firstPoke = 1;

            for (let i = firstPoke; i <= lastPoke; i++) {
                axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
                    .then((response) => {
                        me.pokemons.push(response.data)


                    })
                    .catch((error) => {
                        console.log(error)
                    })
            }



        },
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
}, getLike(pokemon){
    let pkm = pokemon;
    const likeIcon = event.target;
    const likedPokes = this.likedPokes;
    

    if(this.likedPokes.includes(pokemon)){
        console.log('quitandolo de favoritos...');
        this.likedPokes.splice(this.likedPokes.indexOf(pokemon), 1);
        likeIcon.style.fill = '#e0cccc';
       
    }else{
        console.log('añadiendolo a favoritos...');
        
     this.likedPokes.push(pkm);
    
        
    console.log(this.likedPokes);
    likeIcon.style.fill = '#ff0000';
    }
   
    
    
    this.$emit('likedPokes', this.likedPokes);
    

    
}


    },
    mounted() {
        this.getPokemons()
    }

}
</script>
<style>

#pokedex{
    user-select: none;
    
    
    
}
.card {
    
    background-color: #f2f2f2;
    border: 2px solid #f44336; /* Color del borde */
    border-radius: 12px; /* Bordes redondeados */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Sombra suave */
    transition: all 0.3s ease; /* Transición suave en cambios */
    overflow: hidden; /* Oculta el contenido que se desborda */
}

.card:hover {
    transform: translateY(-5px); /* Efecto de elevación al pasar el ratón */
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); /* Sombra más pronunciada */
}

.card-img-top {
    -webkit-user-drag: none;
    width: 100%;
    border-bottom: 2px solid #f44336; /* Línea de separación con borde rojo */
}

.card-body {
    cursor: pointer;
    padding: 1rem; /* Espaciado interno */
}

.card-title {
    font-size: 1.5rem; /* Tamaño del título */
    margin-bottom: 0.5rem; /* Margen inferior */
    color: #333; /* Color del texto del título */
}

.card-text {
    font-size: 1rem; /* Tamaño del texto */
    margin-bottom: 0.25rem; /* Margen inferior */
    color: #555; /* Color del texto */
}

.capitalize {
    text-transform: capitalize;
}

/* Estilo para los tipos de Pokémon */
.card-text .capitalize {
    
    color: black; /* Color del texto blanco */
    padding: 0.25rem 0.5rem; /* Espaciado interno */
    border-radius: 4px; /* Bordes redondeados */
    margin-right: 5px; /* Espacio entre los tipos */
}

.like{
    cursor: pointer;
    height: 45px;
    width: 50px;
}




</style>