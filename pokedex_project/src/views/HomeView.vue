<template>
  <main>
    <div class="container mt-4">
      <div>
        <input type="text" 
          v-model="searchTerm" 
          @input="search"
          placeholder="Buscar Pokemon">
      </div>
    </div>
    <div class="container text-center">
      <div class="row justify-content-md-center">
          <div class="col-sm-12 col-md-6 col-lg-4" 
            v-for="pokemon in copyListPokemons" 
            :key="pokemon.name">
            <CardPokemon
              :name="pokemon.name"
            />
          </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Modal from "@/components/Modal.vue"
import CardPokemon from "@/components/CardPokemon.vue";

let data = ref([])

let pokemons = ref([]);
let copyListPokemons = ref([]);
let offset = 0;
const limit = 20;
let loading = false;
const selectedPokemon = ref(null);
const isModalOpen = ref(false);

const loadPokemons = async () => {
  const response = await fetch(`https://pokeapi.co/api/v2/pokemon?offset=${offset}&limit=${limit}`);
  data = await response.json();
  pokemons.value.push(...data.results);
  copyListPokemons.value.push(...data.results);
  offset += limit;
  loading = false;
};

const openModal = (pokemon) => {
  selectedPokemon.value = pokemon;
  isModalOpen.value = true;
};

const closeModal = () => {
  selectedPokemon.value = null;
  isModalOpen.value = false;
};

const search = () => {
  copyListPokemons.value = [];
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
