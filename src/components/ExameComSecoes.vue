<template>
    <div id="aqui">
        <li class="collection-item" v-for="secao in secoesDetalhadas">
            <div style="cursor: pointer" @click="exibeModal(secao)">
                {{secao.titulo}}
            </div>
        </li>

        <modal v-if="exibirModal"
            :titulo="secaoModal"
            @close="exibirModal = false">
            <div slot="body">
                <div id="chart_div"></div>
            </div>
        </modal>
        
    </div>
</template>

<script>
    import Highcharts from 'highcharts';
    import Modal from './Modal.vue';
    export default {
        props: {
            secoes: Array
        },
        data() {
            return {
                secoesDetalhadas: [],
                exibirModal: false,
                secaoModal: ''
            };
        },
        methods: {
            exibeModal(secao) {
                this.secaoModal = secao.titulo;
                this.exibirModal = true;
                this.criarGrafico();

            },
            criarGrafico() {
                let arraySubexames = [];
                this.sub

                google.charts.load('current', {'packages':['gauge']});
                google.charts.setOnLoadCallback(this.drawChart());
            },
            drawChart(graficos) {

                let arrayGraficos = [
                    ['Label', 'Value']
                ];

                graficos.forEach(
                    g => {
                        arrayGraficos.push(g);
                    }
                );

                var data = google.visualization.arrayToDataTable(g);

                var options = {
                    width: 400, height: 120,
                    redFrom: 90, redTo: 100,
                    yellowFrom:75, yellowTo: 90,
                    minorTicks: 5
                };

                var chart = new google.visualization.Gauge(document.getElementById('chart_div'));

                chart.draw(data, options);

                setInterval(function() {
                    data.setValue(0, 1, 40 + Math.round(60 * Math.random()));
                    chart.draw(data, options);
                }, 13000);
                setInterval(function() {
                    data.setValue(1, 1, 40 + Math.round(60 * Math.random()));
                    chart.draw(data, options);
                }, 5000);
                setInterval(function() {
                    data.setValue(2, 1, 60 + Math.round(20 * Math.random()));
                    chart.draw(data, options);
                }, 26000);

            }
        },
        components: {modal:Modal},
        created() {
            this.secoes.forEach(
                secao => {
                    this.secoesDetalhadas.push({
                        titulo: secao.titulo,
                        showModal: false
                    });
                }
            );
        }
    }
</script>