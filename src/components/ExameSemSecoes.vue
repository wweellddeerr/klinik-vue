<template>
    <div id="graficos"  class="collection-item">

        <div v-for="s in subexames" :id="s.nome" class="col s12 m6 l6">
            <div :id="s.nome + '_gauge'" class="gauge"></div>
            <div id="seasons"></div>
        </div>

        <div class="col s6" id="legenda">
            <br><br><br>
            <div v-for="legenda in legendas">
                <div :style="legenda.estilo"></div>
                {{legenda.nome}}
            </div>
        </div>

    </div>
</template>

<script>
    import Modal from './Modal.vue';
    export default {
        props: {
            subexames: Array,
            resultado: Object,
        },
        data() {
            return {
                legendas: [
                    {estilo: {display: 'inline-block', width: '35px', height: '35px', border: '1px solid', backgroundColor: '#174f00'}, nome: 'Ótimo'},
                    {estilo: {display: 'inline-block', width: '35px', height: '35px', border: '1px solid', backgroundColor: '#8cc83c'}, nome: 'Desejável'},
                    {estilo: {display: 'inline-block', width: '35px', height: '35px', border: '1px solid', backgroundColor: 'yellow'}, nome: 'Limítrofe'},
                    {estilo: {display: 'inline-block', width: '35px', height: '35px', border: '1px solid', backgroundColor: 'orange'}, nome: 'Alto'},
                    {estilo: {display: 'inline-block', width: '35px', height: '35px', border: '1px solid', backgroundColor: 'red'}, nome: 'Muito Alto'}
                ]
            };
        },
        mounted() {

            this.subexames.forEach(

                s => {
                    $('#' + s.nome + '_gauge').dxCircularGauge({
                        scale: {
                            startValue: 0,
                            endValue: s.valorMax,
                            tickInterval: 10,
                            label: {
                                customizeText: function(arg) {
                                    return arg.valueText + s.unidade;
                                }
                            }
                        },
                        rangeContainer: {
                            ranges: s.ranges
                        },
                        tooltip: {
                            enabled: true
                        },
                        title: {
                            text: s.titulo + '<br><p class="subtitulo">(' + this.resultado[s.nome] + ' ' + s.unidade + ')</p>',
                            font: {
                                size: 28
                            }
                        },
                        value: this.resultado[s.nome],
                        //subvalues : [dataSource[0].min, dataSource[0].max]
                    }).dxCircularGauge("instance");
                }
            );
        }
    }
</script>

<style scoped>
    .gauge {
      width: 80%;
      height: 100%;
      float: left;
      margin-bottom: 50px;
    }
    
    #seasons {
      width: 20%;
      float: left;
      text-align: left;
      margin-top: 20px;
    }
</style>