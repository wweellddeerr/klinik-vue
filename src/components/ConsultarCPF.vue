<template>
    <div :class="{'col-xs-offset-3':!cpfInformado, 'col-xs-6': true}">
        <div id="consultarCPF" class="panel panel-primary">
            <div class="panel-heading">
                Consultar CPF


            </div>

            <div class="panel-body">
                <label for="cpf">CPF:</label>
                <input id="cpf" v-model="cpf" :disabled="cpfInformado" type="text" autofocus="true"/>
                <button v-if="cpfInformado" @click="limparCPF">Limpar</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            resultadoFn: Function
        },
        data() {
            return {
                cpf: "",
                cpfInformado: false
            };
        },
        methods: {
            limparCPF() {
                this.cpf = "";
                this.cpfInformado = false;
                this.resultadoFn(null);
            },
            consultarCPF() {
                let url = 'http://klinik-klinik.7e14.starter-us-west-2.openshiftapps.com/pacientes/' + this.cpf;
                this.$http.get(url).then(
                    response => {
                        let paciente = response.data;
                        this.adicionarResultadoHemograma(paciente);
                        this.resultadoFn(paciente);
                    }
                );

            },
            adicionarResultadoHemograma(paciente) {
                paciente.hemacias = 4.84;
                paciente.hemoglobina = 14.1;
                paciente.hematocrito = 39.8;
                paciente.vcm = 82.2;
                paciente.hcm = 29.1;
                paciente.chcm = 35.4;
                paciente.rdw = 11.9;
                paciente.leucocitos = 7800;
                paciente.bastonetes = 0;
                paciente.segmentados = 5070;
                paciente.eosinofilos = 78;
                paciente.basofilos = 0;
                paciente.linfocitos = 2184;
                paciente.monocitos = 468;
                paciente.plaquetas = 254;
                paciente.vmp = 10.8;
                let hemograma = {
                    idadeMaxCrianca: 7,
                    idadeMinIdoso: 70,
                    eritrograma: this.eritrograma(paciente),
                    leucograma: this.leucograma(paciente),
                    seriePlaquetaria: this.seriePlaquetaria(paciente)
                };

                paciente.hemograma = hemograma;
            },
            eritrograma(paciente) {
                return {
                    hemacias: {
                        label: 'Hemácias',
                        unidade: 'milhões/mm3',
                        homemMin: 4.5,
                        homemMax: 6.1,
                        mulherMin: 4,
                        mulherMax: 5.4,
                        criancaMin: 4.07,
                        criancaMax: 5.37,
                        idosoMin: 3.9,
                        idosoMax: 5.36
                    },
                    hemoglobina: {
                        label: 'Hemoglobina',
                        unidade: 'g/dL',
                        homemMin: 13,
                        homemMax: 16.5,
                        mulherMin: 12,
                        mulherMax: 15.8,
                        criancaMin: 10.5,
                        criancaMax: 14,
                        idosoMin: 11.5,
                        idosoMax: 15.1
                    },
                    hematocrito: {
                        label: 'Hematócrito',
                        unidade: '%',
                        homemMin: 36,
                        homemMax: 54,
                        mulherMin: 33,
                        mulherMax: 47.8,
                        criancaMin: 30,
                        criancaMax: 44.5,
                        idosoMin: 33,
                        idosoMax: 46
                    },
                    vcm: {
                        label: 'VCM',
                        unidade: 'fl',
                        homemMin: 80,
                        homemMax: 98,
                        mulherMin: 80,
                        mulherMax: 98,
                        criancaMin: 70,
                        criancaMax: 86,
                        idosoMin: 80,
                        idosoMax: 98
                    },
                    hcm: {
                        label: 'HCM',
                        unidade: 'pg',
                        homemMin: 26.8,
                        homemMax: 32.9,
                        mulherMin: 26.2,
                        mulherMax: 32.6,
                        criancaMin: 23.2,
                        criancaMax: 31.7,
                        idosoMin: 27,
                        idosoMax: 31
                    },
                    chcm: {
                        label: 'CHCM',
                        unidade: 'g/dl',
                        homemMin: 30,
                        homemMax: 36.5,
                        mulherMin: 30,
                        mulherMax: 36.5,
                        criancaMin: 30,
                        criancaMax: 36.5,
                        idosoMin: 30,
                        idosoMax: 36.5
                    },
                    rdw: {
                        label: 'RDW',
                        unidade: '%',
                        homemMin: 11,
                        homemMax: 16,
                        mulherMin: 11,
                        mulherMax: 16,
                        criancaMin: 11,
                        criancaMax: 16,
                        idosoMin: 11,
                        idosoMax: 16
                    }
                };
            },
            leucograma(paciente) {
                return {
                    leucocitos: {
                        unidade: '/mm3',
                        homemMin: 3600,
                        homemMax: 11000,
                        mulherMin: 3600,
                        mulherMax: 11000,
                        criancaMin: 4000,
                        criancaMax: 14000,
                        idosoMin: 3600,
                        idosoMax: 11000
                    },
                    bastonetes: {
                        unidade: '/mm3',
                        homemMin: 0,
                        homemMax: 550,
                        mulherMin: 0,
                        mulherMax: 550,
                        criancaMin: 0,
                        criancaMax: 450,
                        idosoMin: 0,
                        idosoMax: 450
                    },
                    segmentados: {
                        unidade: '/mm3',
                        homemMin: 1480,
                        homemMax: 7700,
                        mulherMin: 1480,
                        mulherMax: 7700,
                        criancaMin: 1200,
                        criancaMax: 9600,
                        idosoMin: 1480,
                        idosoMax: 7700
                    },
                    eosinofilos: {
                        unidade: '/mm3',
                        homemMin: 0,
                        homemMax: 550,
                        mulherMin: 0,
                        mulherMax: 550,
                        criancaMin: 0,
                        criancaMax: 550,
                        idosoMin: 0,
                        idosoMax: 550
                    },
                    basofilos: {
                        unidade: '/mm3',
                        homemMin: 0,
                        homemMax: 220,
                        mulherMin: 0,
                        mulherMax: 220,
                        criancaMin: 0,
                        criancaMax: 300,
                        idosoMin: 0,
                        idosoMax: 220
                    },
                    linfocitos: {
                        unidade: '/mm3',
                        homemMin: 740,
                        homemMax: 5500,
                        mulherMin: 740,
                        mulherMax: 5500,
                        criancaMin: 1520,
                        criancaMax: 10500,
                        idosoMin: 740,
                        idosoMax: 5500
                    },
                    monocitos: {
                        unidade: '/mm3',
                        homemMin: 0,
                        homemMax: 550,
                        mulherMin: 0,
                        mulherMax: 550,
                        criancaMin: 0,
                        criancaMax: 450,
                        idosoMin: 0,
                        idosoMax: 450
                    },
                };
            },
            seriePlaquetaria(paciente) {
                return {
                    plaquetas: {
                        unidade: 'x 10.000/mm3',
                        homemMin: 130,
                        homemMax: 450,
                        mulherMin: 130,
                        mulherMax: 450,
                        criancaMin: 140,
                        criancaMax: 500,
                        idosoMin: 130,
                        idosoMax: 450
                    },
                    vmp: {
                        unidade: '/fl',
                        homemMin: 6.8,
                        homemMax: 12.6,
                        mulherMin: 6.8,
                        mulherMax: 12.6,
                        criancaMin: 6.8,
                        criancaMax: 12.6,
                        idosoMin: 6.8,
                        idosoMax: 12.6
                    }
                };
            }
        },
        watch: {
            cpf() {
                while (this.cpf.length > 0 && isNaN(this.cpf)) {
                    this.cpf = this.cpf.substring(0, this.cpf.length - 1);
                }

                if (this.cpf.length === 11) {
                    this.cpfInformado = true;
                    this.consultarCPF();
                }

            }
        }
    }
</script>

<style>

</style>