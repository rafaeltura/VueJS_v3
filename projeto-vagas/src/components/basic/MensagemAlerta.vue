<template>
    <!-- <div class="alert alert-success" role="alert">
        <h5>Título do alerta</h5>
        <hr>
        <p>Descrição do alerta</p>
    </div> -->
    <!-- <div>
        <slot></slot>
    </div> -->

    <!-- <div class="alert alert-success" role="alert">
        <slot name="titulo"></slot>
        <hr>
        <slot name="descricao"></slot>
        <hr>
        <slot></slot>
    </div> -->

    <div 
        :class="{ 
            alert: true, 
            'alert-success': tipo == 'success',
            'alert-danger': tipo == 'danger'
        }"
        role="alert"
    >
        <slot name="titulo">
            <h3>Título padrão caso o component pai não enviar nada</h3>
        </slot>
        <hr>
        <slot>
            <p>Descrição padrão caso o component pai não enviar nada</p>
        </slot>
    </div>
</template>

<script>
export default {
    name: 'mensagem-alerta',
    props: {
        tipo: {
            type: String,
            default () {
                return 'success';
            }
        }
    }
}
</script>