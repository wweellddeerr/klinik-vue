<template>
    <div  class="row">
      <ul v-if="examesDetalhados.length > 0"
        class="collection with-header col s12"
        v-for="exame in examesDetalhados">
        
        <li class="collection-header"><h4>{{ exame.nome }}</h4></li>
        
        <exame-com-secoes :secoes="exame.secoes" v-if="exame.possuiSecoes"></exame-com-secoes>
        <exame-sem-secoes :subexames="exame.subexames" :resultado="resultado" v-else></exame-sem-secoes>
        
      </ul>
    </div>
</template>

<script>

    import ExameComSecoes from './ExameComSecoes.vue';
    import ExameSemSecoes from './ExameSemSecoes.vue'

    export default {
        props: {
          exames: Array
        },
        data() {
          return {
            examesDetalhados: [],
            resultado: {
              colesterolTotal: 150,
              colesterolLDL: 98,
              colesterolHDL: 52,
              colesterolNaoHDL: 120,
              triglicerideos: 160
            }
          };
        },
        methods: {
          recuperarSecoesOuSubexames(exame) {
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
                {
                  id: 1, 
                  nome: 'colesterolTotal', 
                  titulo: 'Colesterol Total', 
                  sigla: 'Colesterol',
                  unidade: 'mg/dL',
                  valorMax: 300,
                  ranges: [
                    {
                        startValue: 0,
                        endValue: 199,
                        color: "green"
                    },
                    {
                        startValue: 200,
                        endValue: 239,
                        color: "orange"
                    },
                    {
                        startValue: 240,
                        endValue: 300,
                        color: "red"
                    }
                  ]
                },
                {
                  id: 2, 
                  nome: 'colesterolLDL', 
                  titulo: 'Colesterol LDL', 
                  sigla: 'LDL',
                  unidade: 'mg/dL',
                  valorMax: 220,
                  ranges: [
                    {
                        startValue: 0,
                        endValue: 99,
                        color: "#174f00"
                    },
                    {
                        startValue: 100,
                        endValue: 129,
                        color: "#8cc83c"
                    },
                    {
                        startValue: 130,
                        endValue: 159,
                        color: "yellow"
                    },
                    {
                        startValue: 160,
                        endValue: 189,
                        color: "orange"
                    },
                    {
                        startValue: 190,
                        endValue: 220,
                        color: "red"
                    }
                  ]
                },
                {
                  id: 3, 
                  nome: 'colesterolHDL', 
                  titulo: 'Colesterol HDL', 
                  sigla: 'HDL',
                  unidade: 'mg/dL',
                  valorMax: 80,
                  ranges: [
                    {
                        startValue: 0,
                        endValue: 39,
                        color: "red"
                    },
                    {
                        startValue: 40,
                        endValue: 59,
                        color: "yellow"
                    },
                    {
                        startValue: 60,
                        endValue: 80,
                        color: "#8cc83c"
                    }
                  ]
                },
                {
                  id: 4, 
                  nome: 'colesterolNaoHDL', 
                  titulo: 'Colesterol não-HDL', 
                  sigla: 'não-HDL',
                  unidade: 'mg/dL',
                  valorMax: 220,
                  ranges: [
                    {
                        startValue: 0,
                        endValue: 129,
                        color: "#174f00"
                    },
                    {
                        startValue: 130,
                        endValue: 159,
                        color: "#8cc83c"
                    },
                    {
                        startValue: 160,
                        endValue: 189,
                        color: "orange"
                    },
                    {
                        startValue: 190,
                        endValue: 220,
                        color: "red"
                    }
                  ]
                },
                {
                  id: 5, 
                  nome: 'triglicerideos', 
                  titulo: 'Triglicerídeos', 
                  sigla: 'Triglic.',
                  unidade: 'mg/dL',
                  valorMax: 700,
                  ranges: [
                    {
                        startValue: 0,
                        endValue: 149,
                        color: "#8cc83c"
                    },
                    {
                        startValue: 150,
                        endValue: 199,
                        color: "yellow"
                    },
                    {
                        startValue: 200,
                        endValue: 499,
                        color: "orange"
                    },
                    {
                        startValue: 500,
                        endValue: 700,
                        color: "red"
                    }
                  ]
                }
              ];
            }
            
          }
        },
        created() {
          this.exames.forEach(
            exame => {
              let secoesOuSubexames = this.recuperarSecoesOuSubexames(exame);
              if(exame.possuiSecoes) {
                this.examesDetalhados.push({
                  id: exame.id,
                  nome: exame.nome,
                  possuiSecoes: exame.possuiSecoes,
                  secoes: secoesOuSubexames
                });
              }
              else {
                this.examesDetalhados.push({
                  id: exame.id,
                  nome: exame.nome,
                  possuiSecoes: exame.possuiSecoes,
                  subexames: secoesOuSubexames
                });
              }
            }
          );
        },
        components: {
          exameComSecoes: ExameComSecoes,
          exameSemSecoes: ExameSemSecoes
        }
      }
</script>
