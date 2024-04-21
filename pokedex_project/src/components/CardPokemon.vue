<template>
    <div>
        <div class="card">
            <!--<img src="..." class="card-img-top" alt="...">-->
            <div class="card-body">
                <p class="card-text">{{ this.name }}</p>
                <button @click="abrirModal">Abrir Modal</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        name: String
    },

}
</script>