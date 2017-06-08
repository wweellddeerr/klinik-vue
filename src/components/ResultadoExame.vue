<template>
    <div class="panel panel-primary">
        <div class="panel-heading">
            Hemograma

            <button v-if="exibirHemograma" class="glyphicon glyphicon-menu-up pull-right"
                    @click="exibirHemograma = !exibirHemograma">
            </button>
            <button v-else class="glyphicon glyphicon-menu-down pull-right"
                    @click="exibirHemograma = !exibirHemograma"></button>
        </div>
        <div class="panel-body" v-if="exibirHemograma">
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

                    <div class="panel-body" v-show="secaoExame.exibir" v-for="exame in secaoExame.exames">
                        <p>{{ exame.label }}</p>
                        <div class="progress">
                            <div class="progress-bar" style="width: 30%; background-color: firebrick;">
                                < {{ valorMin(secaoExame.nome, exame.nome) }} {{ paciente.hemograma[secaoExame.nome][exame.nome].unidade }}
                                <span v-if="paciente[exame.nome] < valorMin(secaoExame.nome, exame.nome)"
                                    style="border: 5px solid white; background-color: white; color: black;">
                                </span>
                            </div>

                            <div class="progress-bar" style="width: 40%;">
                                Entre {{ valorMin(secaoExame.nome, exame.nome) }} e {{ valorMax(secaoExame.nome, exame.nome) }}
                                {{ paciente.hemograma[secaoExame.nome][exame.nome].unidade }}
                                <span v-if="paciente[exame.nome] >= valorMin(secaoExame.nome, exame.nome) && paciente[exame.nome] <= valorMax(secaoExame.nome, exame.nome)"
                                    style="border: 5px solid white; background-color: white; color: black;">
                                </span>
                            </div>

                            <div class="progress-bar" style="width: 30%; background-color: firebrick;">
                                > {{ valorMax(secaoExame.nome, exame.nome) }} {{ paciente.hemograma[secaoExame.nome][exame.nome].unidade }}
                                <span v-if="paciente[exame.nome] > valorMax(secaoExame.nome, exame.nome)"
                                    style="border: 5px solid white; background-color: white; color: black;">
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </draggable>
        </div>
    </div>
</template>

<script>
    import draggable from 'vuedraggable';

    export default {
        props: ['secoesExame', 'paciente', 'valorMin', 'valorMax'],
        data() {
            return {
                exibirHemograma: true
            };
        },
        components: {draggable}
    }
</script>