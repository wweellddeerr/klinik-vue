<template>
    <div class="row">
        <div class="col-xs-offset-4 col-xs-4">
            <div id="dadosPaciente" class="panel panel-primary">
                <div class="panel-heading">Dados do Paciente</div>
                <div class="panel-body">
                    <label for="nomePaciente">Nome:</label>
                    <input type="text" id="nomePaciente" disabled="true"
                           :value="paciente.nome" size="30">
                    <br>
                    <label for="sexoPaciente">Sexo:</label>
                    <input type="text" id="sexoPaciente" disabled="true"
                        :value="paciente.sexo" size="10">
                    <button @click="$emit('inverterSexo')">Inverter</button>
                    <br>
                    <label for="idadePaciente">Idade:</label>
                    <input type="text" id="idadePaciente" disabled="true"
                        :value="paciente.idade" size="10">
                    <button @click="$emit('aumentarIdade')">+</button>
                    <button @click="$emit('diminuirIdade')">-</button>
                    <br>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['paciente']
    }
</script>