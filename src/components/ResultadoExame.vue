<template>
    <draggable v-model="secoesExame" :options="{group:'people'}" @start="drag=true" @end="drag=false">
        <div v-for="secaoExame in secoesExame" class="panel panel-primary">
            <div class="panel-heading">
                {{secaoExame.titulo}}
                <button v-if="secaoExame.exibir" class="glyphicon glyphicon-menu-up pull-right"
                    @click="secaoExame.exibir = !secaoExame.exibir">
                </button>
                <button v-else class="glyphicon glyphicon-menu-down pull-right"
                    @click="secaoExame.exibir = !secaoExame.exibir"></button>
            </div>

            <div class="panel-body" v-show="secaoExame.exibir">
                Teste
            </div>
        </div>
    </draggable>
</template>

<script>
    import draggable from 'vuedraggable';

    export default {
        data() {
            return {
                secoesExame: [
                    {
                        id: 1,
                        titulo: 'Eritrograma',
                        exibir: false
                    },
                    {
                        id: 2,
                        titulo: 'Leucograma',
                        exibir: false
                    },
                    {
                        id: 3,
                        titulo: 'Série Plaquetária',
                        exibir: false
                    }
                ]
            };
        },
        methods: {
            inverterExibicao(secaoExame) {
                ;
            }
        },
        components: {draggable}
    }
</script>