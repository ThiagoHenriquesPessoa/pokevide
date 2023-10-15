<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import ListPokemons from '../components/ListPokemons.vue';
import CardPokemonSelected from '../components/CardPokemonSelected.vue';

let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/");
let pokemons = reactive( ref() );
let searchPokemonField = ref('');
let pokemonSelected = reactive(ref() );
let loading = ref(false);

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

const selectPokemon = async (pokemon) => {
  loading.value = true;
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelected.value = res)
  .catch(err => alert(err))
  .finally(() => loading.value = false);
}

</script>

<template>
  <main>
    <div class="container text-center">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          <cardPokemonSelected 
            :name="pokemonSelected?.name"
            :xp="pokemonSelected?.base_experience"
            :height="pokemonSelected?.height"
            :img="pokemonSelected?.sprites.other.dream_world.front_default"
            :loading="loading"
            class="text-uppercase"
          />
        </div>
        <div class="col-sm-12 col-md-6">
          <div class="card card-list backList">
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
                :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'" 
                @click="selectPokemon(pokemon)"
                class="text-uppercase"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.backList{
  background: rgb(2,0,36);
  background: radial-gradient(circle, 
              rgba(2,0,36,0.7) 0%,
              rgba(0,212,255,0.7) 0%,
              rgba(44,69,196,0.8) 100%);
}
.card-list{
overflow-y: scroll;
overflow-x: hidden;
max-height: 690px;
}
</style>
