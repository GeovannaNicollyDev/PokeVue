<template>
    <div v-if="isOpen" class="modal">
        <div class="modal-content">
            <span class="close" @click="close">&times;</span>
            <div>
            <h2>{{ selectedItem.name }}</h2>
            <p>Outros dados do Pokémon...</p>
            </div>
        </div>
    </div>
  </template>
  
  <script>
    export default {
      props: ['isOpen', 'selectedItem'],
      methods: {
        close() {
          this.$emit('close');
        }
      }
    };
  </script>
  