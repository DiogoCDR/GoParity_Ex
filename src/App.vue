<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center">
    <PokemonCard />
  </div>
</template>

<script>
import PokemonCard from './components/PokemonCard.vue'

export default {
  components: {
    PokemonCard
  }
}
</script>

<style>
@import './index.css';
</style>
