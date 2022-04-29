<template>
    <div class="card mt-5">
        <div class="card-header bg-dark text-white">
            <div class="row">
                <div class="col d-flex justify-content-between">
                    <div>
                        {{ titulo }}
                    </div>
                    <div>
                        <div class="form-check form-switch">
                            <input type="checkbox" class="form-check-input" v-model="favoritada">
                            <label class="form-check-label">Favoritar</label>
                            <button class="btn btn-danger" @click.prevent="dispararEventoComMitt()">Teste Mitt</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="card-body">
            <p> {{ descricao }}</p>
        </div>
        <div class="card-footer">
            <small class="text-muted">
                Salário: R$ {{ salario }} | Modalidade: {{ getModalidade }} | Tipo: {{ getTipo }} | Publicado em: {{ publicacao }}
            </small>
        </div>
    </div>
</template>

<script>
export default {
    name: 'lista-vaga',
    // props: [
    //     'titulo',
    //     'descricaoVaga',
    //     'salario',
    //     'modalidade',
    //     'tipo',
    //     'publicacao'
    // ]
    // props: {
    //     titulo: String,
    //     descricaoVaga: String,
    //     salario: [ Number, String ],
    //     modalidade: String,
    //     tipo: String,
    //     publicacao: String,
    // }
    props: {
        titulo: {
            type: String,
            required: true,
            validator (valueRecebido) {
                //retorna TRUE se válido ou FALSE se inválido
                console.log('validator da prop.titulo', valueRecebido);
                if (valueRecebido.length > 4) {
                    return true;
                }

                return false;
            }
        },
        descricao: {
            type: String,
            required: true,
        },
        salario: {
            type: [ String, Number ],
            required: true,
        },
        modalidade: {
            type: [ String, Number ],
            required: false,
            default () {
                return '*'.repeat(5);
            }
        },
        tipo: {
            type: [ String, Number ],
            required: false,
            default: ' - '
        },
        publicacao: {
            type: String,
            required: true,
        },
    },
    data () {
        return {
            listaModalidade: [
                {
                    id: 1, descricao: 'Híbrido'
                },
                {
                    id: 2, descricao: 'Home Office'
                },
                {
                    id: 3, descricao: 'Presencial'
                }
            ],
            listaTipo: [
                {
                    id: 1, descricao: 'CLT'
                },
                {
                    id: 2, descricao: 'PJ'
                }
            ],
            favoritada: false
        }
    },
    methods: {
        dispararEventoComMitt () {
            console.log('aqui');
            this.emitter.emit('eventoGlobalMitt','Parametro Com Mitt');
        }
    },
    watch: {
        favoritada (valorNovo) {
            if(valorNovo) {
                this.emitter.emit('vagaFavoritada', this.titulo);
            }else {
                this.emitter.emit('vagaDesfavoritada', this.titulo);
            }
        }
    },
    computed: {
        getModalidade () {
            let descricao = '';
            this.listaModalidade.forEach(modal => {
                if(modal.id == this.tipo) {
                    descricao = modal.descricao;
                }
            });
            return descricao;
        },
        getTipo () {
            switch (this.tipo) {
                case '1':
                    return 'CLT';
                case '2':
                    return 'PJ';
            }
            return '';
        }
    }

}
</script>