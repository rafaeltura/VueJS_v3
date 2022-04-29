<template>
    <div :class="estilo">
        <p>{{ titulo }}</p>
        <h2> {{ valor }} </h2>
    </div>
</template>

<script>
export default {
    name: 'vue-indicador',
    props: [
        'titulo',
        'valor',
        'bg',
        'color'
    ],
    computed: {
        estilo () {
            return `h-100 p-5 rounded-3 border text-center ${this.bg} ${this.color}`;
        }
    }
}
</script>