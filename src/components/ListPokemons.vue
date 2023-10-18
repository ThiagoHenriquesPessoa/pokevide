<script setup>

const pokemon = defineProps(["name", "urlBaseSvg"])

</script>

<template>
  <div class="col-4">
    <div class="card p-2 cardListPokemon">
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
    margin: 5px;
}
.cardListPokemon:hover{
    background: rgb(2,0,36);
    background: radial-gradient(circle, 
                rgba(2,0,36,0.9) 0%,
                rgba(0,212,255,0.9) 0%,
                rgba(44,69,196,1.0) 100%);
}
.cardListPokemon img:hover{
  padding: .1rem;
}
</style>