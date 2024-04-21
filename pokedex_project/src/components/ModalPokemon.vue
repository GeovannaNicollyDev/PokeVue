<template>
  <button @click="abrirModal">Abrir Modal</button>
  <div v-if="abrirFecharModal">
    <div class="modal-dialog modal-dialog-centered">
    ...
    </div>
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
    ...
    </div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      abrirFecharModal: false
    };
  },
  methods: {
    abrirModal() {
      this.abrirFecharModal = !this.abrirFecharModal;
    }
  }
}
</script>



