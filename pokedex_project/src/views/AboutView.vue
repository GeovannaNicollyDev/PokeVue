<template>
  <div class="about">
    {{ $route.params.name }}
  </div>
</template>

<script>
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const loadPokemons = async () => {
  console.log('entrou aqui');
  const response = await fetch($router.params.name);
  console.log(response);
  const data = await response.json();
  pokemons.value.push(...data.results);
  copyListPokemons.value.push(...data.results);
  offset += limit;
  loading = false;
};

export default {
  setup() {
    onMounted(() => {
      loadPokemons();
    });

    return {
      loadPokemons
    };
  },
};
</script>
