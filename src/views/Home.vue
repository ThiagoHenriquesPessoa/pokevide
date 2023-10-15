<script setup>
import { onMounted, reactive, ref} from 'vue';
import ListPokemons from '../components/ListPokemons.vue';

let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/");
let pokemons = reactive( ref() );

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
  .then( res => res.json())
  .then( res => pokemons = res.results )
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
              <ListPokemons 
                v-for="pokemon in pokemons"
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
