<template>
    <div>
        <div class="divBtnVagaFavorita">
            <button class="btn btn-outline-warning" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasRight" aria-controls="offcanvasRight">vagas favoritas</button>
        </div>
        <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
            <div class="offcanvas-header">
                <h5 id="offcanvasRightLabel">Vagas Favoritas</h5>
                <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
            </div>
            <div class="offcanvas-body">
                <p v-show="vagasFavoritas.length == 0">Você não tem vagas favoritas</p>
                <ul class="list-group">
                    <li class="list-group-item" v-for="(titulo, index) in vagasFavoritas" :key="index"> {{ titulo }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'vaga-favorita',
    data () {
        return {
            vagasFavoritas: []
        }
    },
    methods: {
    },
    mounted () {
        this.emitter.on('eventoGlobalMitt', 
            (param) => {
                console.log('Aqui Componente VagaFavorita', param)
            }
        );
        
        this.emitter.on('vagaFavoritada', 
            (titulo) => {
                this.vagasFavoritas.push(titulo);
            }
        );

        this.emitter.on('vagaDesfavoritada', 
            (titulo) => {
                const indiceArray = this.vagasFavoritas.indexof(titulo);
                if (indiceArray != -1) {
                    this.vagasFavoritas.splice(indiceArray, 1);
                }
            }
        );
    }
}
</script>

<style scoped>
    .divBtnVagaFavorita {
        position: absolute; 
        z-index: 1; 
        top: 10px; 
        right: 100px;
    }
</style>