<template>
  <div>
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRnpDDd16-m8fTneCbtEI1TYpDiVqegO11beA&s"
      alt="Pokemon Logo" class="pokemon-logo" />
    <h1 class="titulo1">¿Quién es ese Pokémon?</h1>
    <p class="sub1">Pokémones descubiertos: {{ discoveredCount }}</p>
    <div class="pokemon-grid">
      <PokemonCard v-for="(pokemon, index) in pokemons" :key="index" :pokemon="pokemon" @discovered="increaseCounter" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import PokemonCard from './components/PokemonCard.vue';

export default {
  components: {
    PokemonCard
  },
  data() {
    return {
      pokemons: []
    };
  },
  created() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=20')
      .then(response => {
        this.pokemons = response.data.results.map((pokemon, index) => ({
          name: pokemon.name,
          imageUrl: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`,
          discovered: false
        }));
      });
  },
  methods: {
    increaseCounter() {
      this.discoveredCount++;
    }
  },
  computed: {
    discoveredCount() {
      return this.pokemons.filter(pokemon => pokemon.discovered).length;
    }
  }
};
</script>


<style>
.pokemon-logo {
  display: block;
  margin: 0 auto;
  max-width: 600px;
  height: auto;
}
.pokemon-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Tres columnas de igual ancho */
  gap: 20px; /* Espacio entre tarjetas */
  margin: 20px;
}

.titulo1 {
  text-align: center;
  margin: 0 auto;
  max-width: 600px;
  height: auto;
}

.sub1 {
  text-align: center;
  margin: 0 auto;
  max-width: 300px;
  height: auto;
}



</style>
