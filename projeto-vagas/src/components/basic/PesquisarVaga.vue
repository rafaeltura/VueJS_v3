<template>
    <div class="container">
        <div class="row">
            <div class="col">
                <div class="h-100 p-5 bg-light border rounded-3">
                    
                    <h2>Pesquisar Vagas</h2>

                    <div class="row">
                        <div class="col">
                            <div class="form-group">
                                <label for="">Título da vaga</label>
                                <input type="text" class="form-control" placeholder="Php, pleno, analista" v-model="pesquisaTitulo">
                                <small class="form-text text-muted">Informe palavras relacionadas ao título da vaga desejada</small>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col">
                            <button @click.prevent="pesquisarVaga()" class="btn btn-outline-dark mt-2">
                                Pesquisar
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'pesquisar-vaga',
    data () {
        return {
            pesquisaTitulo: ''
        }
    },
    methods: {
        pesquisarVaga () {
            this.emitter.emit('filtrarVaga', { pesquisarTitulo: this.pesquisaTitulo });
        }
    }
}
</script>
