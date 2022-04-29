<template>
    <div>
        <!-- <topo-padrao @eventoCapturadoNoComponentePai="acaoDoPai($event)"/> -->
        <!-- <topo-padrao @eventoCapturadoNoComponentePai="$event()"/> -->
        <!-- <topo-padrao @eventoCapturadoNoComponentePai="$event('Texto 1', 5567)"/> -->
        <!-- <topo-padrao :funcaoCallback="acaoDoPai"/> -->
        <vaga-favorita />
        <topo-padrao @navegar="paraComponente = $event"/>
        
        <!-- <mensagem-alerta v-if="exibirMensagemAlerta"/> -->

        <!-- <mensagem-alerta v-if="true">
            <div class="alert alert-success" role="alert">
                <h5>Título do alerta</h5>
                <hr>
                <p>Descrição do alerta</p>
            </div>
        </mensagem-alerta> -->
        
        <!-- <mensagem-alerta v-if="true">
            <template v-slot:titulo>
                <h5>Título do alerta</h5>
            </template>
            <template v-slot:descricao>
                <p>Descrição do alerta</p>
            </template>
        </mensagem-alerta> -->

        <!-- <mensagem-alerta v-if="true">

            <h3>Teste no ínicio com Slot Padrao</h3>
            
            <template v-slot:titulo>
                <h5>Título do alerta</h5>
            </template>
            
            <div>
                <p>Teste no meio com Slot Padrão</p>
            </div>

            <template v-slot:descricao>
                <p>Descrição do alerta</p>
            </template>

            <ul>
                <li>Teste com li no fim com Slot Padrão</li>
                <li>Teste com li no fim com Slot Padrão</li>
                <li>Teste com li no fim com Slot Padrão</li>
            </ul>
        </mensagem-alerta> -->

        <!-- <mensagem-alerta v-if="true">
        </mensagem-alerta> -->

        <mensagem-alerta v-if="exibirMensagemAlerta" :tipo="tipoMensagem">
            <template v-slot:titulo>
                <h5> {{ tituloMensagem }}</h5>
            </template>
            <p> {{ descricaoMensagem }} </p>
        </mensagem-alerta>

        <conteudo-pagina v-if="estaMontado" :pagina="paraComponente"/>
        <!-- <button @click.prevent="montarDesmontarConteudo()"> beforeUnmount/Unmounted em conteudoPagina</button> -->
        
    </div>
</template>

<script>
import ConteudoPagina from './components/layouts/ConteudoPagina.vue';
import MensagemAlerta from './components/basic/MensagemAlerta.vue';
import TopoPadrao from './components/layouts/TopoPadrao.vue';
import VagaFavorita from './components/basic/VagaFavorita.vue';

export default {
  name: 'App',
  components: {
    ConteudoPagina,
    MensagemAlerta,
    TopoPadrao,
    VagaFavorita,
  },
  data () {
      return {
          estaMontado: true,
          paraComponente: 'home-main',
          exibirMensagemAlerta: false,
          tipoMensagem: 'success',
          tituloMensagem: '',
          descricaoMensagem: ''
      }
  },
  methods: {
    //   montarDesmontarConteudo () {
    //       this.estaMontado = !this.estaMontado;
    //   },
    //   acaoDoPai (paramDoFilho) {
    //       console.log('Chegou no PAAAPAAAIII', paramDoFilho)
    //   }
    //   acaoDoPai (a, b) {
    //       console.log('Function Callback definida no componente pai e chamada no componente filho');
    //       console.log(a, b);
    //   }
  },
  mounted () {
    //   this.emitter.on('mensagemAlerta',
    //     () => {
    //         this.exibirMensagemAlerta = true;
    //         setTimeout(() => {
    //             this.exibirMensagemAlerta = false;
    //         }, 5000);
    //     }
    //   );

    this.emitter.on('mensagemAlerta', 
        ( { tipo, titulo, descricao } ) => {
            this.tipoMensagem = tipo;
            this.tituloMensagem = titulo;
            this.descricaoMensagem = descricao;

            this.exibirMensagemAlerta = true;
            setTimeout(() => {
                this.exibirMensagemAlerta = false;
            }, 5000);
    })
  }
}
</script>

<style scoped>
</style>
