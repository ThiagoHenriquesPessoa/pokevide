<script setup>

const pokemon = defineProps([ "name", "xp", "height", "img", "loading" ])
</script>

<template>
  <div 
    class="card CardPokemonSelected">
    <img 
      v-if="pokemon.name"
      :src="pokemon?.img" 
      height="543"
      class="card-img-top pt-2" 
      :alt="pokemon?.name"
    >

    <img 
      v-else
      src="../assets/egg_pokemon.svg" 
      height="543"
      class="card-img-top pt-2" 
      alt="???"
    >

    <h1>
      {{ pokemon?.name || "???"}}
    </h1>
    <div class="card-body">
      <hr>
      <div class="row">
        <section class="col">
          <strong>XP: </strong>
          <span>{{ pokemon?.xp }}</span>
        </section>
        <section class="col">
          <strong>Altura: </strong>
          <span>{{ pokemon?.height }}</span>
        </section>
      </div>
    </div>
  </div>
</template>



<style scoped>
.CardPokemonSelected{
    background: rgb(2,0,36);
    background: radial-gradient(circle, 
                rgba(2,0,36,0.7) 0%,
                rgba(0,212,255,0.7) 0%,
                rgba(44,69,196,0.8) 100%);
    cursor: pointer;
}
.animate__animated.animate__flipIny {
    --animate-duration: 2s;
  }
</style>