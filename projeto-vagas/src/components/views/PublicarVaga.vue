<template>
    <div class="container py-4">
        <!-- <h1>Componente PublicarVaga</h1> -->
        <div class="row">
            <div class="col">
                <h4>Cadastre a sua vaga para milhares de profissionais e de graça</h4>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <label class="form-label">Título</label>
                <input v-model="titulo" type="text" class="form-control" placeholder="Programador JavaScript e VueJS" />
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <label class="form-label">Descrição</label>
                <textarea v-model="descricao" class="form-control" placeholder="Detalhes da vaga" ></textarea>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <label class="form-label">Salário</label>
                <input v-model="salario" type="number" class="form-control" />
            </div>
            <div class="col">
                <label class="form-label">Modalidade</label>
                <select v-model="modalidade" class="form-select">
                    <option value="" disabled>Selecione uma opção</option>
                    <option value="1">Híbrido</option>
                    <option value="2">Home Office</option>
                    <option value="3">Presencial</option>
                </select>
            </div>
            <div class="col">
                <label class="form-label">Tipo</label>
                <select v-model="tipo" class="form-select">
                    <option value="" disabled>Selecione uma opção</option>
                    <option value="1">CLT</option>
                    <option value="2">PJ</option>
                </select>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <button class="btn btn-success" @click.prevent="salvarVaga()">Publicar</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'publicar-vaga',
        data () {
            return {
                titulo: '',
                descricao: '',
                salario: 0,
                modalidade: '',
                tipo: '',
                vagas: JSON.parse(localStorage.getItem('vagas')) || []
            }
        },
        methods: {
            salvarVaga () {
                if ( this.validarForm() ) {
                    this.vagas.push({
                        titulo: this.titulo,
                        descricao: this.descricao,
                        salario: this.salario,
                        modalidade: this.modalidade,
                        tipo: this.tipo,
                        publicacao: this.getCurrentDate()
                    })
                    localStorage.setItem('vagas', JSON.stringify(this.vagas));

                    // this.emitter.emit('mensagemAlerta');
                    this.emitter.emit('mensagemAlerta', {
                        tipo: 'success',
                        titulo: 'Cadastro realizado com sucesso!',
                        descricao: `Parabéns, agora a vaga ${this.titulo} estará disponível para milhares de profissionais!`
                    });

                    this.limparForm();

                }else {

                    this.emitter.emit('mensagemAlerta', {
                        tipo: 'danger',
                        titulo: 'OPSS! Não foi possível realizar o cadastro!',
                        descricao: 'Parece que você esqueceu de preencher alguma informação obrigatória.'
                    });
                }
            },
            getCurrentDate () {
                const now = new Date();
                return now.toLocaleDateString('pt-BR');
            },
            validarForm () {
                
                if (this.titulo != '' || this.descricao != '' || !!this.salario) {
                    return true;
                }

                return false;
            },
            limparForm () {
                this.titulo = '';
                this.descricao = '';
                this.salario = 0;
                this.modalidade = '';
                this.tipo = '';
            }
        }
    }
</script>

<style>

</style>