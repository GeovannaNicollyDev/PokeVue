<template>
    <main>
      <div class="container mt-4">
        <div>
          <input type="text" v-model="searchTerm" @input="search" placeholder="Digite para buscar">
        </div>
        <div class="row">
          <div class="col-md-6">
            <ul class="list-group">
              <li class="list-group-item" v-for="pokemon in copyListPokemons" :key="pokemon.name">
                {{ pokemon.name }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </main>
  </template>

<script setup>
import { ref, onMounted } from "vue";

let data = ref([])

let pokemons = ref([]);
let copyListPokemons = ref([]);
let offset = 0;
const limit = 20;
let loading = false;

const loadPokemons = async () => {
  loading = true;
  const response = await fetch(`https://pokeapi.co/api/v2/pokemon?offset=${offset}&limit=${limit}`);
  data = await response.json();
  pokemons.value.push(...data.results);
  copyListPokemons.value.push(...data.results);
  offset += limit;
  loading = false;
};

const search = () => {
  copyListPokemons.value = []
  if (searchTerm.value !== "") {
    const filteredData = pokemons.value.filter(pokemon => pokemon.name.toLowerCase().includes(searchTerm.value.toLowerCase()));
    copyListPokemons.value.push(...filteredData);
    console.log(pokemons)
  } else {
    offset = 0
    pokemons.value = []
    loadPokemons();
  }
};
const searchTerm = ref('');

const handleScroll = () => {
  if (loading) return;
  const bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;
  if (bottomOfWindow) {
    loadPokemons();
  }
};

onMounted(() => {
  loadPokemons();
  window.addEventListener('scroll', handleScroll);
});

</script>