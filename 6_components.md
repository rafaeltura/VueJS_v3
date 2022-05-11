## 1. Components

*Single File Component* (Componente de Arquivo Único) ou *Single File Template* (Modelo de Arquivo Único).
Correspondem a menor parte da interface front-end, com suas próprias características e comportamentos, ou seja,
são pequenas partes da interface de uma aplicação com responsabilidades únicas e bem estruturados, permitindo que sejam reutilizados de forma prática em diversas partes da aplicação.

### 1.1. Montagem
- Dentro da tag ou chave (depende da abordagem utilizada para montar um component) ``` template ```, é necessário ao menos um elemento html. Em caso de vários elementos html que estejam na mesma hierarquia, deve-se agrupa-los em um elemento pai, exemplo:

    - <span style="color:red">Errado:</span>
    ~~~javascript
    //Nota: Perceba que aqui os elementos estão na mesma hierarquia, ou seja, todos são irmãos.
        template: ` <h1> Título </h1> 
                    <small> Pequena descrição </small> 
                    <section> 
                        <p> Parágrafo 1</p>
                        <p> Parágrafo 2</p>
                    </section>` 
    ~~~

    - <span style="color:green">Correto:</span>
    ~~~javascript 
    //Nota: Perceba que aqui todos os elementos irmãos estão dentro de um elemento pai.
        template: ` <div>
                        <h1> Título </h1>
                        <small> Pequena descrição </small>
                        <section> 
                            <p> Parágrafo 1</p>
                            <p> Parágrafo 2</p>
                        </section>
                    </div>` 
    ~~~

### 1.2. Nomenclatura

- A definição do nome de um componente no javascript e no html irá depender da estrutura e/ou do padrão adotado do projeto.
  - Pode ser PascalCase: ```File: ComponenteUm.vue ```, ```Html: <ComponenteUm /> ou <ComponenteUm></ComponenteUm> ```;
  - Pode ser kebab-case (este mais recomendado para HTML): ```Html: <componente-um/> ou <componente-um></componente-um>```;

### 1.3. Renderização dinâmica de componentes

- Para ter uma renderização dinâmica de componentes, por exemplo, ora renderizar componente X e ora renderizar componente Y no mesmo espaço, utiliza-se a seguinte tag:
~~~html
    <component :is="nomeComponenteParaSerRenderizado"/>
~~~
- Recurso normalmente utilizado em guias de navegação

### 1.4. Manter componente ativado/desativado

- Normalmente o componente é montado e desmontado a cada renderização. Com os lifecycles activated e deactivated o componente é 'mantido vivo' em cachê, gerando menos processamento.
- Para conseguir manter vivo componente(s) em determinada parte da aplicação é necessário usar a seguinte tag com os componentes aninhados dentro:
~~~html
    <keep-alive>
        <componente-um />
        <componente-dois />
    </keep-alive>
~~~
-Pode ser utilizado também com a [renderização dinâmica](file:///home/rafaeltura/projetos/VueJS/VueJS_v3/6_components.md#renderiza%C3%A7%C3%A3o-din%C3%A2mica-de-componentes):
~~~html
    <keep-alive>
        <component :is="nomeComponenteParaSerRenderizado"/>
    </keep-alive>
~~~

### 1.5. Comunicação entre Componentes
- Esta comunicação é importante para conseguirmos customizar os componentes filhos no instante que são inicializados no componente pai. Com isso, temos uma comunicação prática e direta.

#### 1.5.1. De PAI para FILHO
- Encaminhar valores do componente PAI para o componente FILHO:
  - Para isso, o componente filho utiliza a chave ``` props ```, no js, para definir os parâmetros que aceita receber do componente pai via atributos no html:
  
    ###### NOMENCLATURA DAS PROPS:
    
    - As nomenclaturas das ``` props ``` <strong> <mark>não</mark> </strong> podem ser iguais as nomenclaturas das chaves do objeto ``` data ``` desse componente filho, ou seja, se houver uma prop denominada 'teste', no objeto ``` data ``` não poderá ter uma chave com esse mesmo nome. Pois, as chaves das props trabalham de forma análoga as chaves do data. 
  
    - No js o ideal é utilizar o padrão ``` camelCase ```, mais abaixo será visto que no html o ideal é o ``` kebab-case ```. Apesar dessa diferença de padrões das nomenclaturas o ``` Vue ``` tem inteligência suficiente para encontrá-las, por isso, não haverá inconsistência.
    - No html, onde esse componente é chamado, utiliza-se essas props definidas como se fossem atributos do html (value, type, ...), por isso, o padrão de nomenclatura desses atributos seja o ``` kebab-case ```:
   
      - Exemplo básico de definição das props e ao envio de informações fixas, sem vinculo direto com o objeto data do componente pai 
        ~~~html
            <!-- Código do template do componente PAI ocultado -->
            <componente-filho 
                propriedade-um="Texto/número/objeto/array/boolean..."
                propriedade-dois="Essas propriedades estão recebendo infos fixas, ou seja, não possuem vinculo direto com o component pai"
            />
        ~~~
     - Exemplo básico de definição de props no js: 
        ~~~javascript
            props: ['propriedadeUm', 'propriedadeDois'] //exemplo 1 de como definir
        ~~~

    ###### FORMAS DE ENVIAR INFORMAÇÕES AO COMPONENTE FILHO

    - As ``` props ``` recebidas com base em chaves do objeto ``` data ``` do componente Pai (atributos monitorados pela instância do componente pai) permanacem **reativos**, ou seja, caso o atributo do componente pai sofra alguma alteração, no controle do pai, essa alteração é replicada para o componente filho, mas o oposto só ocorre se a propriedade for definida como **two-way**.
    - Na subseção [Tipagem](file:///home/rafaeltura/projetos/VueJS/VueJS_v3/6_components.md#tipagem-das-props) é possível ver os tipos permitidos. 
      - <mark>COM</mark> REATIVIDADE: utiliza-se o **v-bind** na prop desejada, para ter essa passagem de atributos pai para as props do componente filho:
      ~~~html
            <!-- 
                SUPONDO QUE:
                atributoXDoPai = 'Teste X'
                atributoYDoPai = 90
             -->
           <componente-filho
                :propriedade-um="atributoXDoPai" 
                :propriedade-dois="atributoYDoPai"
            />
      ~~~
      ~~~javascript
            props: [
                'propriedadeUm' //chegará 'Teste X'
                'propriedadeDois' //chegará 90
            ]
      ~~~

      - <mark>SEM</mark> REATIVIDADE: apenas informa-se as propriedades e os valores fixos delas:
      ~~~html
           <componente-filho
                propriedade-um="Qualquer coisa" 
                propriedade-dois="100"
            />
      ~~~
      ~~~javascript
            props: [
                'propriedadeUm' //chegará 'Qualquer coisa'
                'propriedadeDois' //chegará 100
            ]
      ~~~

      - enviando callback via prop:
      ~~~html
        <componente-filho :functionCallback="methodDoComponentePai">
      ~~~
      ~~~javascript
      //JS do componente pai
        methods: {
            methodDoComponentePai (param1 = 'não', param2 = 'não', param3 = 'não') {
                console.log('Executada dentro do componente filho, via prop: ', param1, param2, param3);
            }
        }
      ~~~
      ~~~javascript
      //JS do componente filho
        props: {
            functionCallback: {
                type: Function
            }
        }
      ~~~
      - Para executa-las dentro do componente filho, essa prop, pode ser atribuida por exemplo a um evento de click dentro do componente filho:
        ~~~html
        <!-- HTML do template do componente filho  -->
            <button @click="functionCallback()"> Teste </button>
            <!-- inclusive podem ser passados parametros -->
            <button @click="functionCallback('parametro1', 'parametro2', '...')"> Teste </button>
        ~~~
    
    ###### TIPAGEM DAS PROPS

    - Recurso que permite determinar qual ou quais tipos de dados determinada prop poderá receber.
    - Tipagens disponíveis => **Array, Boolean, Date, Function, Number, Object, String e Symbol**
      - JS: 
        ~~~javascript
        /*  
        Nota: agora a 'props' será definida como um objeto, 
            então, a definição interna será na dotação de object, 
            ou seja, chave: valor. 
        */
            props: {
                tituloTeste: String,
                estaAtivo: Boolean,
                quantidade: Number,
                dataAtivacao: Date,
                infosExtras: Object,
                itens: Array,
                functionCallback: Function,
                qualquerCoisa: [String, Number, ...]
            }
        ~~~

    ###### VALIDAÇÃO DE PROPS

    - É possível realizar validações para determinada prop:
      - Utilizando o atributo ``` required ``` é possível definir que a propriedade é obrigatória ou não, por default a definição é ``` required: false ```.
      - Enquanto com o ``` validator ``` é possível executar uma function customizada com determinada regra/lógica.
      - JS:
      ~~~javascript
        props: {
            tituloTeste: { //Torna um outro objeto
                type: String, //Nota-se que agora a inferência de tipagem mudou, utilizando uma chave type: tipoDeDado esperado.
                required: true, // Apenas TRUE ou FALSE
                validator (value) {// irá retornar true para válido e false para inválido
                    console.log('Validator tituloTeste', value);
                    if ( value.trim() && value.length > 3){
                        return true;
                    }

                    return false;
                }
            },
            estaAtivo: Boolean,
            quantidade: Number,
            qualquerCoisa: {
                type: [String, Number, ...]
            },
        }
      ~~~ 

    ###### VALORES DEFAULT

    - A partir do atributo ``` default ``` é possível definir valores padrões para determinada propriedade. Para isso, a propriedade precisa estar em formato de objeto literal.
    - O atributo ``` default ``` pode receber um valor fixo de acordo com o tipo (se existir tipagem) ou uma function com alguma lógica.
    - JS:
    ~~~javascript
        props: {
            tituloTeste: {
                type: String,
                required: true,
                validator (value) {
                    console.log('Validator tituloTeste', value);
                    if ( value.trim() && value.length > 3){
                        return true;
                    }

                    return false;
                }
            },
            estaAtivo: {
                type: Boolean,
                default: false,
            },
            quantidade: Number,
            qualquerCoisa: {
                type: [String, Number],
                default () {
                    return '*'.repeat(20);
                },
            },
        }
    ~~~


#### 1.5.2. De FILHO para PAI
- Para isso ocorrer, precisará combinar a emissão de eventos do componente filho para o componente pai de modo que o componente pai possa capturar esses eventos emitidos pelo componente filho, lidar e tratar com essa comunicação.
    
    ###### $EMIT e V-ON/@
    - Nos ``` methods ``` do componente filho, é criada uma function qualquer, e sua implementação será:
    - enviando parâmetros:
        ~~~javascript
            methods: {
                teste () {
                    this.$emit('nomeEventoNaTAGComponenteFilho', 'parametros1', 2, ['3']);
                    /**
                     * sendo =>
                    *       this = instância vue que está sendo executada, no caso instância do componente filho
                    *       $emit = function do próprio vue, a qual recebe:
                    *                1° argumento = nome do evento informado na tag do componente filho
                    *                2° ou mais = parâmetros opcionais
                    *                
                    * /
                }
            }
        ~~~
        
        - Na chamada do componente filho, a partir da tag html, é necessário add a diretiva ``` v-on/@ ``` chamando o nome do evento que foi passado como 1° argumento da function $emit 
        ~~~html
            <!-- código html onde chama o componente filho -->
            <componente-filho @nomeEventoNaTAGComponenteFilho="nomeMethodNoComponentePai($event)"/>
            <!-- Sendo assim, o $emit irá disparar o evento do v-on e o qual irá executar o method definido no componente pai, e o $event será o responsável por carregar os parametros para o pai, caso tenham sido passados. -->
        ~~~

        - Nos ``` methods ``` do componente pai terá que ter o methdo que foi chamado na tag do componente filho, no exemplo acima, o method é **nomeMethodNoComponentePai**
        ~~~javascript
            methods: {
                nomeMethodNoComponentePai (parametros) {
                    console.log('Parametros definidos lá no $emit do componente filho', parametros);
                }
            } 
        ~~~

    - enviando function Callback:
      ~~~javascript
      //JS do componente filho sendo executado no methods do componente pai e sendo executado diretamente via $event
        teste2 () {
            this.$emit('nomeEventoTagComponenteFilho',
                () => {
                    console.log('aqui a function de callback enviado pelo componente filho');
                }
            );
        }
      //JS do componente filho sendo executado diretamente via $event e recebendo parametros
        teste3 () {
            this.$emit('nomeEventoTagComponenteFilho',
                (param1, param2) => {
                    console.log('aqui a function de callback do componente filho sendo executada pelo $event e recebendo os paramestros: ', param1, param2);
                }
            );
        }
      ~~~
      ~~~html
      <!-- Chamada da tag componente filho chamando um method componente pai-->
        <componente-filho @nomeEventoTagComponenteFilho="methodComponentePai($event)">
      <!-- Chamada da tag componente filho executando a callback sem a necessidade de um method no componente pai-->
        <componente-filho @nomeEventoTagComponenteFilho="$event()">
      <!-- Chamada da tag componente filho executando a callback e passando parametros, sem a necessidade de um method no componente pai-->
        <componente-filho @nomeEventoTagComponenteFilho="$event('Texto 1', 200)"> 
      ~~~   
      ~~~javascript
      // Method do componente PAI
        methods: {
            methodComponentePai (callback) {
                callback();
            }
        }    
      ~~~
    
#### 1.5.3. Comunicação Indireta entre Componentes
- Esse caso é para qndo há a necessidade de componentes irmãos ou componentes de alguma parte da aplicação precisam se comunicar.
- Para conseguir estabeler essa comunicação com componentes distantes, ou seja, uma comunicação indireta, há diversas abordagens:
  - via localStorage, fazendo ele a ponte entre componentes;
  - via props enviando uma function de callback sendo passadas de pai para filhos até o componente desejado;
  - via evento personalizada do componente filho passando pelos componentes pais fazendo alguma ação no componente pai do elemento desejado capaz de afeta-lo, seria o caminho inverso das props, ou seja, $emit;
  - via framework de estado que é o VUEX;
  - via barramento de evento global: mitt, uma biblioteca inclusive recomendada pela doc do vue 3;
  - em versões anteriores do VUE utilizava-se a abordagem com ``` eventBus ```;

### 1.6. SLOTS
- Maneira de passar conteúdo HTML para do componente pai para o componente filho.
- tag reservada do Vue.

    ###### tag SLOT
    - Todo conteúdo informado entre as tags de abertura e fechamento do componente filho serão recebidas no template desse componente por meio da tag ``` <slot> </slot> ```;
    ~~~html 
    <!-- Tags do componente filho, aninhando outros elementos html -->
        <componente-alerta>
            <div class="alert alert-success" role="alert">
                <h3> Título do alerta </h3>
                <hr />
                <p> Descrição do alerta </p>
            </div>
        </componente-alerta>
    ~~~ 
    ~~~html
    <!-- Template da criação do componente alerta -->
        <template>
            <div>
                <slot></slot>
            </div>
        </template>
    ~~~

    ###### Múltiplos SLOT's ou SLOT's Nomeados
    - Técnica que permite trabalhar com vários slots e cada qual receberá um determinado html.
    - Para isso utiliza-se ``` <template v-slot:nomeDoSlot> código html </template> ``` na chamada do componente e na criação html desse componente utiliza-se ``` <slot name='nomeDoSlot'> </slot> ```.
    - A ordem dos templates na chamada do componente não importam, pois, a definição da ordem de renderização é realizada na criação desse componente, ou seja, a ordem dos slots é que importa.
    - Caso haja, na criação do componente, slots com mesmo name duplicados, o conteúdo tbm será duplicado.
    ~~~html 
    <!-- Tags do componente filho, aninhando outros elementos html -->
        <componente-alerta>
            <template v-slot:descricao>
                <p> Descrição do alerta </p>
            </template>
            <template v-slot:titulo>
                <h3> Título do alerta </h3>
            </template>
        </componente-alerta>
    ~~~ 
    ~~~html
    <!-- Template da criação do componente alerta -->
        <template>
            <div class="alert alert-success" role="alert">
                <slot name='titulo'> </slot>     
                <hr />
                <slot name='descricao'> </slot> 
            </div>
        </template>
    ~~~

    ###### SLOT geral
    - Utilizado para quando haja conteúdo html sem estar nomeado, dessa forma, todo esse conteúdo será direcionado para um slot geral.
    ~~~html 
    <!-- Tags do componente filho, aninhando outros elementos html -->
        <componente-alerta>
            
            <h3> Teste slot geral </h3>

            <template v-slot:titulo>
                <h3> Título do alerta </h3>
            </template>

            <div>
                <p><strong>Descrição do slot geral</strong></p>
            </div>

            <template v-slot:descricao>
                <p> Descrição do alerta </p>
            </template>
            
            <ul>
                <li>Item 1</li>
                <li>Item 2</li>
                <li>...</li>
            </ul>
            
        </componente-alerta>
    ~~~ 
    ~~~html
    <!-- Template da criação do componente alerta -->
        <template>
            <div class="alert alert-success" role="alert">
                <slot name='titulo'> </slot>     
                <hr />
                <slot name='descricao'> </slot> 
                
                <hr />
    <!-- Aqui ficarão os elementos que não estão mapeados, independente da posição deles dentro da chamada do componente -->
                <slot></slot> 
            
            </div>
        </template>
    ~~~

    ###### SLOT com Valores DEFAULT
    - Podemos definir valores default para os slot's para que qndo não haja conteúdo sendo enviado para eles, exiba determinada informação default.
     ~~~html 
    <!-- Tags do componente filho, aninhando outros elementos html -->
        <componente-alerta>
            <!-- <template v-slot:titulo>
                <h3> Título da mensagem </h3>
            </template>
            <p> Descrição da mensagem </p> -->
        </componente-alerta>
    ~~~ 
    ~~~html
    <!-- Template da criação do componente alerta -->
        <template>
            <div class="alert alert-success" role="alert">
                <slot name='titulo'> 
                    <h3> Título default </h3>
                </slot>     
                <hr />
                <slot> 
                    <p>Descrição default</p>
                </slot> 
            </div>
        </template>
    ~~~

