<template>
  <div id="app" class="container">
    <h3>
      Meus Resultados de Exames
    </h3>
    
    <div v-if="resultados.length > 0">
      <ul v-for="res in resultados" class="collection">
        <li class="collection-item avatar" 
          @click="res.exibir=!res.exibir" style="cursor: pointer;">
          <i class="material-icons circle material-icons">assignment</i>
          <span class="title">{{ res.data }}</span>
          <p>
            {{ res.medico }}
          </p>
        </li>
        <li>
          <resultado v-show="res.exibir" :exames="res.exames"></resultado>
        </li>
      </ul>
    </div>
    <h3 v-else>Nenhum resultado disponível</h3>
  </div>
</template>

<script>

  import Resultado from './components/Resultado.vue'
  export default {
    name: 'app',
    data () {
      return {
        resultados: []
      };
    },
    methods: {
      carregarResultados() {
        //simula carregar os resultados do paciente -> /paciente/1/resultados
        let resultadosServico = [
          {
            id: 1, 
            data: '03/05/2017', 
            medico: 'Dr. Getúlio Bernardo',
            exames: [
              {id: 1, nome: 'Hemograma', possuiSecoes:true},
              {id: 2, nome: 'Lipidograma', possuiSecoes:false}
            ]
          },
          {
            id: 2, 
            data: '25/11/2016', 
            medico: 'Dr. Erik Neves',
            exames: [
              {id: 1, nome: 'Hemograma', possuiSecoes:true}
            ]
          },
          {
            id: 3, 
            data: '14/09/2016', 
            medico: 'Dr. Leandro Cotta',
            exames: [
              {id: 1, nome: 'Hemograma', possuiSecoes:true}
            ]
          },
          {
            id: 4, 
            data: '11/01/2016', 
            medico: 'Dr. Fulano',
            exames: [
              {id: 1, nome: 'Hemograma', possuiSecoes:true}
            ]
          }
        ];
        let visivel = true;
        resultadosServico.forEach(
          r => {
            this.resultados.push({
              id: r.id,
              data: r.data,
              medico: r.medico,
              exames: r.exames,
              exibir: visivel
            });
            visivel = false;
          }
        );
      }
    },
    created() {
      this.carregarResultados();
    },
    components: {
      resultado: Resultado
    }
  }
</script>

<style>

</style>
