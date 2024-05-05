<template>
    <div>
      <h1 class="text-center">Pokedex</h1>
      
        
  
      <div class="container"id="pokedex">
        
        <button class="btn btn-light" @click="showAll()">Show all</button>
        <button class="btn m-1 ml-3" v-for="type in typeName" :style="{ backgroundColor: getColor(type)}  " @click="filterByType(type)" > 
            {{ type.toUpperCase() }}
        </button>
        <button class="btn btn-light" @click="filterByTeam()" >Show team</button>

        <Selector @filter-by-id="updateFilter" />
        
        
        <div class="row mt-3">
          
            
            <div class="card col-3 m-5 align-content-center " v-for="pokemon in filteredPokemons" :key="pokemon.id">
                

                <svg  @click="getLike(pokemon)"  class="like mt-3"xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 512 512">
		<path fill="#e0cccc" d="m47.6 300.4l180.7 168.7c7.5 7 17.4 10.9 27.7 10.9s20.2-3.9 27.7-10.9l180.7-168.7c30.4-28.3 47.6-68 47.6-109.5v-5.8c0-69.9-50.5-129.5-119.4-141c-45.6-7.6-92 7.3-124.6 39.9l-12 12l-12-12c-32.6-32.6-79-47.5-124.6-39.9C50.5 55.6 0 115.2 0 185.1v5.8c0 41.5 17.2 81.2 47.6 109.5" />
	</svg>
    <input type="checkbox" class="btn-check teamcheck" :id="'btn-check-outlined-' + pokemon.id" v-model="pokemon.caught" @change="toggleCaught(pokemon)">
            <label class="btn btn-outline-primary team" :for="'btn-check-outlined-' + pokemon.id">{{ pokemon.caught ? 'RELEASE' : 'CATCH' }}</label><br>
   
   
              <img :src="pokemon.sprites.front_default" class="card-img-top" alt="...">
              
              <div class="card-body">
                <h5 class="card-title capitalize">{{ pokemon.name }}</h5>
                <p class="card-text">Pokedex Number: {{ pokemon.id }}</p>
                <p class="card-text">Height: {{ pokemon.height }}</p>
                <p class="card-text">Weight: {{ pokemon.weight }}</p>
                <p class="card-text ">Types:
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
import Selector from './Selector.vue'

export default {
    components: {
        Selector
    },

    data() {
        return {
            pokemons: []
            ,
            likedPokes: [],
            typeName: ['normal', 'fire', 'water', 'electric', 'grass', 'ice', 'fighting', 'poison', 'ground', 'flying', 'psychic', 'bug', 'rock', 'ghost', 'dragon', 'dark', 'steel', 'fairy'],
            selectedType: null,
            showFavComponent: false,
            pokemonTeam :[],
            showTeam : false,
            showNumbers: false,
            idSearch: [],
            
        }
    },
    computed: {
        filteredPokemons(){
            if (this.showTeam) {
                return this.pokemons.filter(pokemon => pokemon.caught)
            } else if (this.selectedType) {
                return this.pokemons.filter(pokemon => pokemon.types.some(type => type.type.name === this.selectedType))
            } else if(this.showNumbers){
                console.log(this.idSearch);
               
                return this.pokemons.filter(pokemon => pokemon.id >= this.idSearch[0] && pokemon.id <= this.idSearch[1]);                
            }
            else {
                return this.pokemons
            }
        }
    },
    methods: {
        showAll(){
            this.showTeam = false;
            this.selectedType = null;
            this.showNumbers = false;
        },
        updateFilter(id){
            
            this.showNumbers = true;
            // console.log(id);
           let hola= id.split('-');
            // console.log(hola);
            this.idSearch = hola;
           
            console.log('updating filter...');
            console.log(this.showNumbers);
            // console.log(id);
        },
        toggleCaught(pokemon) {

            
            if(pokemon.caught){
                this.pokemonTeam.push(pokemon);
                console.log('añadiendo a equipo a ' + pokemon.name);
             }else{
                this.pokemonTeam.splice(this.pokemonTeam.indexOf(pokemon), 1);
                console.log('quitando de equipo a ' + pokemon.name);
                
            }
            
            


           
            //  pokemon.caught = true;

            //  this.pokemonTeam.push(pokemon);
            
          
             console.log(this.pokemonTeam);
            

        },
        filterByTeam(){
            this.showTeam = true;
         this.selectedType = null;
         this.showNumbers = false;
        },
       

        getPokemons() {
            const me = this;

            const lastPoke = 151;
            const firstPoke = 1;

            for (let i = firstPoke; i <= lastPoke; i++) {
                axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
                    .then((response) => {
                        response.data.caught = false;
                        me.pokemons.push(response.data)


                    })
                    .catch((error) => {
                        console.log(error)
                    })
            }



        },
        filterByType(type){
            console.log(type);
            this.selectedType = type;
            this.showTeam = false;
            this.showNumbers = false;
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

.team-check {
        /* Ajusta el tamaño del checkbox */
        transform: scale(0.8);
        margin-right: 2px; 
    }

    .team {
        position: absolute ;
        align-content: center;
        top: 15px;
        right: 15px;
        width: 52px;
        height: 40px;

        font-size: 12px;
        padding: 0.2rem 0.4rem; 
    }




</style>