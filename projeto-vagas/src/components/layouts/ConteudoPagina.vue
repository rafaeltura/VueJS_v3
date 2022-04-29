<template>
    <div>
        <h1>{{ titulo }}</h1>
        <!-- <button @click.prevent="atualizarComponente()"> beforeUpdate/Updated </button> <br /> -->
        <!-- Ações apra renderização Dinâmica -->
        <!-- <button @click.prevent="irPara = 'home-main'">
            ir para HomeMain
        </button>
        <button @click.prevent="irPara = 'publicar-vaga'">
            ir para PublicarVaga
        </button> -->
        
        <!-- keep-alive: Preservar a instância de cada componente para não destruir e recria-los a cada iteração -->
        <!-- component: Renderizar de modo dinâmico os componentes HomeMain e PublicarVaga -->
        <keep-alive>
            <component :is="pagina" />
        </keep-alive>
        
            <!-- <home-main></home-main>
            <publicar-vaga></publicar-vaga> -->
    </div>
</template>

<script>
    import HomeMain from '../views/HomeMain.vue';
    import PublicarVaga from '../views/PublicarVaga.vue';

    export default {
        name: 'conteudo-pagina',
        props: {
            pagina: {
                type: String,
                required: true
            }
        },
        components: {
            HomeMain,
            PublicarVaga
        },
        data () {
            return {
                teste: 'chave do obj data',
                titulo: 'Componente ConteudoPagina',
            }
        },
        // methods: {
        //     atualizarComponente () {
        //         this.titulo += '*';
        //     },
        // },
        // beforeCreate () {
        //     console.log('conteudo-pagina -> ANTES de criar', this.teste);
        // },
        // created () {
        //     console.log('conteudo-pagina -> CRIADO', this.teste, this);
        // },
        // beforeMount () {
        //     console.log('conteudo-pagina -> ANTES de montar o template podemos, por exemplo, consumir os dados do backend por meio de uma requisição e atribuir os dados e registros');
        // },
        // mounted () {
        //     console.log('conteudo-pagina -> MONTADO');
        // },
        // beforeUpdate () {
        //     console.log('conteudo-pagina -> ANTES de atualizar', this.titulo);
        // },
        // updated () {
        //     console.log('conteudo-pagina -> ATUALIZADO', this.titulo);
        // },
        // beforeUnmount () {
        //     console.log('conteudo-pagina -> ANTES de desmontar/destruir');
        // },
        // unmounted () {
        //     console.log('conteudo-pagina -> DESMONTADO / DESTRUIDO');
        // },
    /*    errorCaptured () {
            console.log('conteudo-pagina -> ERRO Capturado');
        },
        renderTracked () {
            console.log('conteudo-pagina -> Re-renderização RASTREADA');
        },
        renderTriggered () {
            console.log('conteudo-pagina -> Re-renderização ATIVADA');
        },
        actived () {
            console.log('conteudo-pagina -> ATIVADO');
        },
        deactivated () {
            console.log('conteudo-pagina -> DESATIVADO');
        }
    */

    }
</script>

<style>
</style>