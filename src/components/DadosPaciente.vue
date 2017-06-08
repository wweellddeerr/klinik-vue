<template>
    <div class="col-xs-6">
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
                <label for="hemaciasPaciente">{{ paciente.hemograma.eritrograma.hemacias.label }}:</label>
                <input type="text" id="hemaciasPaciente" disabled="true"
                       :value="paciente.hemacias" size="10">
                <button @click="$emit('aumentarHemacias')">+</button>
                <button @click="$emit('diminuirHemacias')">-</button>

                <br>
                <label for="hemoglobinaPaciente">{{ paciente.hemograma.eritrograma.hemoglobina.label }}:</label>
                <input type="text" id="hemoglobinaPaciente" disabled="true"
                       :value="paciente.hemoglobina" size="10">
                <button @click="$emit('aumentarHemoglobina')">+</button>
                <button @click="$emit('diminuirHemoglobina')">-</button>

                <br>
                <label for="hematocritoPaciente">{{ paciente.hemograma.eritrograma.hematocrito.label }}:</label>
                <input type="text" id="hematocritoPaciente" disabled="true"
                       :value="paciente.hematocrito" size="10">
                <button @click="$emit('aumentarHematocrito')">+</button>
                <button @click="$emit('diminuirHematocrito')">-</button>

                <br>
                <label for="vcmPaciente">{{ paciente.hemograma.eritrograma.vcm.label }}:</label>
                <input type="text" id="vcmPaciente" disabled="true"
                       :value="paciente.vcm" size="10">
                <button @click="$emit('aumentarVCM')">+</button>
                <button @click="$emit('diminuirVCM')">-</button>

                <br>
                <label for="hcmPaciente">{{ paciente.hemograma.eritrograma.hcm.label }}:</label>
                <input type="text" id="hcmPaciente" disabled="true"
                       :value="paciente.hcm" size="10">
                <button @click="$emit('aumentarHCM')">+</button>
                <button @click="$emit('diminuirHCM')">-</button>

                <br>
                <label for="chcmPaciente">{{ paciente.hemograma.eritrograma.chcm.label }}:</label>
                <input type="text" id="chcmPaciente" disabled="true"
                       :value="paciente.chcm" size="10">
                <button @click="$emit('aumentarCHCM')">+</button>
                <button @click="$emit('diminuirCHCM')">-</button>

                <br>
                <label for="rdwPaciente">{{ paciente.hemograma.eritrograma.rdw.label }}:</label>
                <input type="text" id="rdwPaciente" disabled="true"
                       :value="paciente.rdw" size="10">
                <button @click="$emit('aumentarRDW')">+</button>
                <button @click="$emit('diminuirRDW')">-</button>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['paciente']
    }
</script>