<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import ListPokemons from '../components/ListPokemons.vue';

let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/");
let pokemons = reactive( ref() );
let searchPokemonField = ref('');

onMounted(async () => {
  try {
    const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0");
    const data = await response.json();
    pokemons.value = data.results;
  } catch (error) {
    console.error("Erro ao carregar os Pokémon:", error);
  }
});

const pokemonFiltered = computed(() => {
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon => 
    pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value;
});

</script>

<template>
  <main>
    <div class="container text-center">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          <div class="card" style="width: 18rem;">
            <img src="https://www.ensino.eu/media/3kyh4vko/pokemon.jpg?width=500&height=500" class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">Card title </h5>
              <p class="card-text"> Some content </p>
            </div>
          </div>
        </div>
        <div class="col-sm-12 col-md-6">
          <div class="card">
            <div class="card-body row">
              <div class="mb-3">
                <label 
                  hidden 
                  for="searchPokemonField" 
                  class="form-label">
                  Pesquisar...
                </label>
                
                <input 
                  v-model="searchPokemonField"
                  type="text" 
                  class="form-control" 
                  id="searchPokemonField" 
                  placeholder="Ex.: pikachu">
              </div>

              <ListPokemons 
                v-for="pokemon in pokemonFiltered"
                :key="pokemon.name" 
                :name="pokemon.name"
                :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
