<template>
  <div class="container">
    <consultar-cpf :resultadoFn="exibirResultadoConsulta"></consultar-cpf>
    <dados-paciente v-if="pacienteRecuperado"
            :paciente="pacienteRecuperado"
            @inverterSexo="inverterSexo"
            @aumentarIdade="aumentarIdade"
            @diminuirIdade="diminuirIdade">
    </dados-paciente>
    <br></br>
    <resultado-exame v-if="pacienteRecuperado"></resultado-exame>
  </div>
</template>

<script>

  import ConsultarCPF from './components/ConsultarCPF.vue';
  import DadosPaciente from './components/DadosPaciente.vue';
  import ResultadoExame from './components/ResultadoExame.vue';

  export default {
    data() {
      return {
        pacienteRecuperado: null
      };
    },
    methods: {
      exibirResultadoConsulta(paciente) {
        this.pacienteRecuperado = paciente;
      },
      inverterSexo() {
        if(this.pacienteRecuperado.sexo === 'Masculino') {
          this.pacienteRecuperado.sexo = 'Feminino';
        }
        else {
          this.pacienteRecuperado.sexo = 'Masculino';
        }
      },
      aumentarIdade() {
        if(this.pacienteRecuperado.idade <= 120) {
          this.pacienteRecuperado.idade++;
        }
      },
      diminuirIdade() {
        if(this.pacienteRecuperado.idade > 0) {
          this.pacienteRecuperado.idade--;
        }
      }
    },
    components: {
      consultarCpf: ConsultarCPF,
      dadosPaciente: DadosPaciente,
      resultadoExame: ResultadoExame
    }
  }
</script>

<style>

</style>
