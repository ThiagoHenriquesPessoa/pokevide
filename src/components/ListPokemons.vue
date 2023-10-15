<script setup>

const pokemon = defineProps(["name", "urlBaseSvg"])

</script>

<template>
  <div class="col-4">
    <div class="card p-2 mb-3 cardListPokemon">
      <p class="text-center"> 
        {{ pokemon.name }}
      </p>
      <img 
        :src="urlBaseSvg" class="card-img-top" 
        alt="..." 
        height="80" />
    </div>
  </div>
</template>

<style scoped>
.cardListPokemon{
    background: rgb(2,0,36);
    background: radial-gradient(circle, 
                rgba(2,0,36,0.7) 0%,
                rgba(0,212,255,0.7) 0%,
                rgba(44,69,196,0.8) 100%);
    cursor: pointer;
}
.cardListPokemon:hover{
    background: rgb(2,0,36);
    background: radial-gradient(circle, 
                rgba(2,0,36,0.8) 0%,
                rgba(0,212,255,0.8) 0%,
                rgba(44,69,196,0.9) 100%);
}
.cardListPokemon img:hover{
  padding: .1rem;
}
</style>