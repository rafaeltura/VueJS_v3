<template>
    <div class="container">
        <div class="row">
            <div class="col-6 bg-light">
                <span class="fs-4">ENTRADA DE DADOS</span>
                <hr>
                <form>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Nome:</label>
                        <div class="col">
                            <input 
                                type="text"
                                class="form-control"
                                v-model.lazy="form.nome"
                            >
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">E-mail:</label>
                        <div class="col">
                            <input
                                type="email"
                                class="form-control"
                                v-model="form.email"
                            >
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Senha:</label>
                        <div class="col">
                            <input 
                                type="password" 
                                class="form-control"
                                v-model.trim="form.senha"
                            >
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Idade:</label>
                        <div class="col">
                            <input 
                                type="number"
                                class="form-control"
                                v-model="form.idade"
                            >
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Gênero:</label>
                        <div class="col">
                            <div class="form-check form-check-inline">
                                <input 
                                    class="form-check-input" 
                                    type="radio"
                                    v-model="form.genero"
                                    value="F"
                                >
                                <label class="form-check-label">
                                    Feminino
                                </label>
                            </div>
                            <div class="form-check form-check-inline">
                                <input 
                                    class="form-check-input" 
                                    type="radio"
                                    v-model="form.genero"
                                    value="M"
                                >
                                <label class="form-check-label">
                                    Masculino
                                </label>
                            </div>
                        </div>
                    </div>

                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Licença:</label>
                        <div class="col">
                            <div class="form-check form-switch">
                                <input
                                    class="form-check-input"
                                    type="checkbox"
                                    v-model="form.licenca"
                                    true-value="S"
                                    false-value="N"
                                >
                                <label class="form-check-label">Li e aceito os termos</label>
                            </div>
                        </div>
                    </div>

                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Interesses:</label>
                        <div class="col">
                            <div class="form-check">
                                <input 
                                    class="form-check-input"
                                    type="checkbox"
                                    v-model="form.interesses"
                                    value="JS"
                                >
                                <label class="form-check-label">
                                    JavaScriot
                                </label>
                            </div>
                            <div class="form-check">
                                <input 
                                    class="form-check-input"
                                    type="checkbox"
                                    v-model="form.interesses"
                                    value="VUE"
                                >
                                <label class="form-check-label">
                                    VueJS
                                </label>
                            </div>
                            <div class="form-check">
                                <input 
                                    class="form-check-input"
                                    type="checkbox"
                                    v-model="form.interesses"
                                    value="A"
                                >
                                <label class="form-check-label">
                                    Angular
                                </label>
                            </div>
                            <div class="form-check">
                                <input 
                                    class="form-check-input"
                                    type="checkbox"
                                    v-model="form.interesses"
                                    value="NODE"
                                >
                                <label class="form-check-label">
                                    NodeJS
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Telefone:</label>
                        <div class="col">
                            <input type="tel" class="form-control" pattern="[0-9]{2} [0-9]{5}-[0-9]{4}">
                            <small class="text-muted">Formato: 11 97777-5555</small>
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Data:</label>
                        <div class="col">
                            <input type="date" class="form-control">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Data/hora local:</label>
                        <div class="col">
                            <input type="datetime-local" class="form-control">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Mês:</label>
                        <div class="col">
                            <input type="month" class="form-control">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Semana:</label>
                        <div class="col">
                            <input type="week" class="form-control">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Hora:</label>
                        <div class="col">
                            <input type="time" class="form-control">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Cor:</label>
                        <div class="col">
                            <input type="color" class="form-color">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Valor limite:</label>
                        <div class="col">
                            <input type="range" class="form-range" min="0" max="100" step="1">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Escondido:</label>
                        <div class="col">
                            <input type="hidden" class="form-control">
                        </div>
                    </div>
                    <div class="mb-3 row">
                        <label class="col-3 col-form-label">Upload:</label>
                        <div class="col">
                            <input type="file" class="form-control">
                        </div>
                    </div>
                    <hr>
                    <div class="mb-3 row">
                        <div class="col d-flex justify-content-between">
                            <button class="btn btn-secondary" type="reset">Limpar</button>
                            <button class="btn btn-success" type="button">Enviar (btn)</button>
                            <button class="btn btn-success" type="submit">Enviar (submit)</button>
                        </div>                        
                    </div>
                   
                </form>
            </div>

            
            <div class="col-6 text-white bg-secondary">
                <span class="fs-4">ESTADO DO OBJETO</span>
                <hr>
                <div class="mb-5 row">
                    <span>{{ form }}</span>
                </div>

                <span class="fs-4">SAÍDA DE DADOS</span>
                <hr>
                <div class="mb-3 row">
                    <span>Nome: {{ form.nome }} </span>
                </div>
                <div class="mb-3 row">
                    <span>E-mail: {{ form.email }} </span>
                </div>
                <div class="mb-3 row">
                    <span>Senha: {{ form.senha }} </span>
                </div>
                <div class="mb-3 row">
                    <span>Idade: {{ form.idade }}</span>
                </div>
                <div class="mb-3 row">
                    <span>Gênero: {{ form.genero }}</span>
                </div>
                <div class="mb-3 row">
                    <span>Licença: {{ form.licenca }}</span>
                </div>
                <div class="mb-3 row">
                    <span>Interesses:</span>
                    <ul>
                        <li v-for="(interesse, index) in form.interesses" :key="index">{{ interesse }}</li>
                    </ul>
                </div>
                <div class="mb-3 row">
                    <span>Telefone:</span>
                </div>
                <div class="mb-3 row">
                    <span>Data:</span>
                </div>
                <div class="mb-3 row">
                    <span>Data/hora local:</span>
                </div>
                <div class="mb-3 row">
                    <span>Mês:</span>
                </div>
                <div class="mb-3 row">
                    <span>Semana:</span>
                </div>
                <div class="mb-3 row">
                    <span>Hora:</span>
                </div>
                <div class="mb-3 row">
                    <span>Cor:</span>
                </div>
                <div class="mb-3 row">
                    <span>Valor limite:</span>
                </div>
                <div class="mb-3 row">
                    <span>Escondido:</span>
                </div>
                <div class="mb-3 row">
                    <span>Upload:</span>
                </div>  
            </div>
        </div>

    </div>

</template>

<script>
export default {
    name: 'Formulario',
    data () {
        return {
            form:{
                nome: 'Rafael',
                email: 'teste@teste.com.br',
                senha: '123456',
                idade: 90,
                licenca: 'N',
                interesses: ['JS', 'VUE'],
                genero: 'M'
            }
        }
    }
}
</script>
