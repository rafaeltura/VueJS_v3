<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand" href="#">Vagas</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <!-- <li class="nav-item">
                        <a class="nav-link" href="#" @click.prevent="navegarPara()">home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" @click.prevent="navegarPara()">publicar vaga</a>
                    </li> -->
                    <!-- <li class="nav-item">
                        <a class="nav-link" href="#" @click.prevent="funcaoCallback('Teste 1', 200)">home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" @click.prevent="funcaoCallback('Teste 2', 300)">publicar vaga</a>
                    </li> -->
                    <li class="nav-item">
                        <a class="nav-link" href="#" @click.prevent="navegarPara('home-main')">home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" @click.prevent="navegarPara('publicar-vaga')">publicar vaga</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
    export default {
        name: 'topo-padrao',
        // props: {
        //     funcaoCallback: Function
        // }
        // methods: {
        //     navegarPara () {
        //         // this.$emit(nomeDoEventoCapturadoNoComponentePai, opcional(objeto, string, callback));
        //         // this.$emit('eventoCapturadoNoComponentePai', 'Parametros Enviados do Componente Filho');
        //         // this.$emit('eventoCapturadoNoComponentePai', () => console.log('Função de callback do Filho'));
        //         // this.$emit('eventoCapturadoNoComponentePai', (a, b) => console.log('Função de callback do Filho com parametros', a, b));
        //     }
        // }
        methods: {
            navegarPara (para) {
                this.$emit('navegar', para);
            }
        }
    }
</script>

<style>
</style>