<template>
  <div class="custom-container">
    <h1 class="main-title">Pokémon</h1>
    <div v-if="pokemon" class="custom-padding">
      <img :src="pokemon.sprites.front_default" alt="Pokemon Image" class="custom-image" />
      <div class="custom-title">
        <h2 class="pokemon-name">{{ capitalizeFirstLetter(pokemon.name) }}</h2>
        <p class="custom-hp">HP: {{ pokemon.stats[0].base_stat }}</p>
        <div class="custom-types-container">
          <span
            v-for="type in pokemon.types"
            :key="type.slot"
            :class="['custom-type', typeColor(type.type.name)]"
          >
            {{ type.type.name }}
          </span>
        </div>
      </div>
      <button @click="fetchPokemon" class="custom-button mt-4">New Pokémon!</button>
    </div>
    <div v-else class="custom-loading">Loading...</div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      pokemon: null
    }
  },
  created() {
    this.fetchPokemon()
  },
  methods: {
    async fetchPokemon() {
      try {
        const randomId = Math.floor(Math.random() * 898) + 1
        const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${randomId}`)
        this.pokemon = response.data
      } catch (error) {
        console.error('Error fetching Pokémon data:', error)
      }
    },
    typeColor(type) {
      const colors = {
        fire: 'bg-fire',
        water: 'bg-water',
        grass: 'bg-grass',
        electric: 'bg-electric',
        ice: 'bg-ice',
        fighting: 'bg-fighting',
        poison: 'bg-poison',
        ground: 'bg-ground',
        flying: 'bg-flying',
        psychic: 'bg-psychic',
        bug: 'bg-bug',
        rock: 'bg-rock',
        ghost: 'bg-ghost',
        dark: 'bg-dark',
        dragon: 'bg-dragon',
        steel: 'bg-steel',
        fairy: 'bg-fairy'
      }
      return colors[type] || 'bg-gray-500' // Default to gray if type is not found
    },
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    }
  }
}
</script>
