<template>
    <div  class="row">
      <ul v-if="examesDetalhados.length > 0"
        class="collection with-header col s12"
        v-for="exame in examesDetalhados">
        
        <li class="collection-header"><h4>{{ exame.nome }}</h4></li>
        
        <li class="collection-item" v-for="secao in exame.secoes">
          <div>
            {{secao.titulo}}
            <a href="#!" class="secondary-content">
              <i class="material-icons">send</i>
            </a>
          </div>
        </li>
      </ul>
    </div>
</template>

<script>
    export default {
        props: {
          exames: Array
        },
        data() {
          return {
            examesDetalhados: []
          };
        },
        methods: {
          recuperarSecoesExame(exame) {
            //simula recuperar seções por exame: GET /exames/{exame.id}/secoes
            if(exame.id === 1) {
              //hemograma
              return [
                {
                  id: 1,
                  nome: 'eritrograma',
                  titulo: 'Eritrograma',
                  exibir: true,
                  exames: [
                    {nome: 'hemacias', label: 'Hemácias'},
                    {nome: 'hemoglobina', label: 'Hemoglobina'},
                    {nome: 'hematocrito', label: 'Hematócrito'},
                    {nome: 'vcm', label: 'VCM'},
                    {nome: 'hcm', label: 'HCM'},
                    {nome: 'chcm', label: 'CHCM'},
                    {nome: 'rdw', label: 'RDW'}
                  ]
                },
                {
                  id: 2,
                  nome: 'leucograma',
                  titulo: 'Leucograma',
                  exibir: true,
                  titulo: 'Leucograma',
                  exames: [
                    {nome: 'leucocitos', label: 'Leucócitos'},
                    {nome: 'bastonetes', label: 'Bastonetes'},
                    {nome: 'segmentados', label: 'Segmentados'},
                    {nome: 'eosinofilos', label: 'Eosinófilos'},
                    {nome: 'basofilos', label: 'Basófilos'},
                    {nome: 'linfocitos', label: 'Linfócitos'},
                    {nome: 'monocitos', label: 'Monócitos'}
                  ]
                },
                {
                  id: 3,
                  nome: 'seriePlaquetaria',
                  titulo: 'Série Plaquetária',
                  exibir: true,
                  exames: [
                      {nome: 'plaquetas', label: 'Plaquetas'},
                      {nome: 'vmp', label: 'VMP'}
                  ]
                }
              ];
            }
            else if(exame.id === 2) {
              //lipidograma
              return [
                {id: 1, nome: ''}
              ];
            }
            
          }
        },
        created() {
          this.exames.forEach(
            exame => {
              let secoes = this.recuperarSecoesExame(exame);
              this.examesDetalhados.push({
                id: exame.id,
                nome: exame.nome,
                secoes: secoes
              });
            }
          );
        }
      }
</script>
