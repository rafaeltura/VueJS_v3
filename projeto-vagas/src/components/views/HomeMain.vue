<template>
    <div class="container py-4">
        <!-- <h1>Componente HomeMain</h1> -->
        <pesquisar-vaga />
        
        <div class="row mt-5">
            <div class="col">
                <!-- <lista-vaga 
                    v-for="( {titulo, descricao, salario, modalidade, tipo, publicacao}, index ) in vagas"
                    :key="index"
                    :titulo="titulo"
                    :descricao-vaga="descricao"
                    :salario="salario"
                    :modalidade="modalidade"
                    :tipo="tipo"
                    :publicacao="publicacao"
                /> -->
                <lista-vaga v-for="(vaga, index) in vagas" :key="index" v-bind="vaga" />
            </div>
        </div>

        <div class="row mt-5">
            <div class="col-4">
                <vue-indicador bg="bg-dark" color="text-white" titulo="Vagas abertas" valor="25" />
            </div>
            <div class="col-4">
                <vue-indicador bg="bg-dark" color="text-white" titulo="Profissionais cadastrados" valor="225" />
            </div>
            <div class="col-4">
                <vue-indicador bg="bg-light" color="text-dark" titulo="Usuários online" :valor="usuariosOnline" />
            </div>
        </div>
    </div>
</template>

<script>
    import ListaVaga from '../basic/Vaga.vue';
    import PesquisarVaga from '../basic/PesquisarVaga.vue';
    import VueIndicador from '../basic/Indicador.vue';

    export default {
        name: 'home-main',
        components: {
            ListaVaga,
            PesquisarVaga,
            VueIndicador
        },
        data () {
            return {
                usuariosOnline: 0,
                vagas: []
            }
        },
        methods: {
            getUsuariosOnline () {
                this.usuariosOnline = Math.floor(Math.random() * 101); //entre 0 e 100
            },
            getVagas () {
                return JSON.parse(localStorage.getItem('vagas')) || []
            },
            filtrarVagas (pesquisarTitulo) {
                const vagas = JSON.parse(localStorage.getItem('vagas')) || [];
                this.vagas = vagas.filter( (vaga) => vaga.titulo.toLowerCase().includes(pesquisarTitulo.toLowerCase()));
            }
        },
        created () {
            setInterval(this.getUsuariosOnline, 1000);
            this.vagas = this.getVagas();
        },
        activated () {
            this.vagas = this.getVagas();
        },
        mounted () {
            this.emitter.on('filtrarVaga', ( { pesquisarTitulo } ) => {
                this.filtrarVagas(pesquisarTitulo);
            });
        },
        // deactivated () {
        //     console.log('home-main -> DESATIVADO');
        // },
        // beforeUnmount () {
        //     console.log('home-main -> ANTES de desmontar/destruir');
        // },
        // unmounted () {
        //     console.log('home-main -> DESMONTADO / DESTRUIDO');
        // },
    }
</script>

<style>
</style>