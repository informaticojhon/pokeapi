<template>
    <div>
      <img :src="pokemonImage" :class="{'blur': !pokemon.discovered}">
      <input v-if="!pokemon.discovered" v-model="guess" @keydown.enter="checkGuess" />
      <button v-if="!pokemon.discovered" @click="checkGuess">Descubrir</button>
      <p v-if="pokemon.discovered">{{ pokemon.name }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: ['pokemon'],
    data() {
      return {
        guess: '',
      };
    },
    methods: {
      checkGuess() {
        if (this.guess.toLowerCase() === this.pokemon.name.toLowerCase()) {
          this.pokemon.discovered = true;
          this.$emit('discovered', this.pokemon);
        } else {
          alert("Nombre incorrecto");
        }
      }
    },
    computed: {
      pokemonImage() {
        return this.pokemon.imageUrl;
      }
    }
  };
  </script>
  
  <style scoped>
  .blur {
    filter: blur(5px) grayscale(100%);
    column-count: 3;
      
  }
  </style>
  