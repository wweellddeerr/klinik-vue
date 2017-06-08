<template>
    <div class="container">
        <div class="row">
            <consultar-cpf :resultadoFn="exibirResultadoConsulta"></consultar-cpf>
            <dados-paciente v-if="pacienteRecuperado"
                            :paciente="pacienteRecuperado"
                            @inverterSexo="inverterSexo"
                            @aumentarIdade="aumentarIdade"
                            @diminuirIdade="diminuirIdade"
                            @aumentarHemacias="aumentarHemacias"
                            @diminuirHemacias="diminuirHemacias"
                            @aumentarHemoglobina="aumentarHemoglobina"
                            @diminuirHemoglobina="diminuirHemoglobina"
                            @aumentarHematocrito="aumentarHematocrito"
                            @diminuirHematocrito="diminuirHematocrito"
                            @aumentarVCM="aumentarVCM"
                            @diminuirVCM="diminuirVCM"
                            @aumentarHCM="aumentarHCM"
                            @diminuirHCM="diminuirHCM"
                            @aumentarCHCM="aumentarCHCM"
                            @diminuirCHCM="diminuirCHCM"
                            @aumentarRDW="aumentarRDW"
                            @diminuirRDW="diminuirRDW">
            </dados-paciente>
        </div>
        <br></br>
        <resultado-exame v-if="pacienteRecuperado"
                         :secoesExame="secoesExame"
                         :paciente="pacienteRecuperado"
                         :valorMin="valorMin"
                         :valorMax="valorMax"
                         :isCriancaFn="isCrianca">

        </resultado-exame>

    </div>
</template>

<script>

    import ConsultarCPF from './components/ConsultarCPF.vue';
    import DadosPaciente from './components/DadosPaciente.vue';
    import ResultadoExame from './components/ResultadoExame.vue';

    export default {
        data() {
            return {
                pacienteRecuperado: null,
                secoesExame: [
                    {
                        nome: 'eritrograma',
                        exibir: true,
                        titulo: 'Eritrograma',
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
                        nome: 'leucograma',
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
                        nome: 'seriePlaquetaria',
                        exibir: true,
                        titulo: 'Série Plaquetária',
                        exames: [
                            {nome: 'plaquetas', label: 'Plaquetas'},
                            {nome: 'vmp', label: 'VMP'}
                        ]
                    }
                ]
            };
        },
        methods: {
            valorMin(secao, nomeExame) {
                if (this.pacienteRecuperado.hemograma[secao][nomeExame]) {
                    if (this.isCrianca()) {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].criancaMin;
                    }
                    else if (this.isIdoso()) {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].idosoMin;
                    }
                    else if (this.pacienteRecuperado.sexo === 'Masculino') {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].homemMin;
                    }
                    else {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].mulherMin;
                    }
                }
            },
            valorMax(secao, nomeExame) {
                if (this.pacienteRecuperado.hemograma[secao][nomeExame]) {
                    if (this.isCrianca()) {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].criancaMax;
                    }
                    else if (this.isIdoso()) {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].idosoMax;
                    }
                    else if (this.pacienteRecuperado.sexo === 'Masculino') {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].homemMax;
                    }
                    else {
                        return this.pacienteRecuperado.hemograma[secao][nomeExame].mulherMax;
                    }
                }
            },
            exibirResultadoConsulta(paciente) {
                this.pacienteRecuperado = paciente;
            },
            isCrianca() {
                return this.pacienteRecuperado.idade <= this.pacienteRecuperado.hemograma.idadeMaxCrianca;
            },
            isIdoso() {
                return this.pacienteRecuperado.idade >= this.pacienteRecuperado.hemograma.idadeMinIdoso;
            },
            inverterSexo() {
                if (this.pacienteRecuperado.sexo === 'Masculino') {
                    this.pacienteRecuperado.sexo = 'Feminino';
                }
                else {
                    this.pacienteRecuperado.sexo = 'Masculino';
                }
            },
            aumentarIdade() {
                if (this.pacienteRecuperado.idade <= 120) {
                    this.pacienteRecuperado.idade++;
                }
            },
            diminuirIdade() {
                if (this.pacienteRecuperado.idade > 0) {
                    this.pacienteRecuperado.idade--;
                }
            },
            aumentarHemacias() {
                this.pacienteRecuperado.hemacias = this.corrigirCasasDecimais(this.pacienteRecuperado.hemacias + 0.1);
            },
            diminuirHemacias() {
                if (this.pacienteRecuperado.hemacias > 0) {
                    this.pacienteRecuperado.hemacias = this.corrigirCasasDecimais(this.pacienteRecuperado.hemacias - 0.1);
                }
            },
            aumentarHemoglobina() {
                this.pacienteRecuperado.hemoglobina = this.corrigirCasasDecimais(this.pacienteRecuperado.hemoglobina + 0.1);
            },
            diminuirHemoglobina() {
                if (this.pacienteRecuperado.hemoglobina > 0) {
                    this.pacienteRecuperado.hemoglobina = this.corrigirCasasDecimais(this.pacienteRecuperado.hemoglobina - 0.1);
                }
            },
            aumentarHematocrito() {
                this.pacienteRecuperado.hematocrito = this.corrigirCasasDecimais(this.pacienteRecuperado.hematocrito + 0.1);
            },
            diminuirHematocrito() {
                if (this.pacienteRecuperado.hematocrito > 0) {
                    this.pacienteRecuperado.hematocrito = this.corrigirCasasDecimais(this.pacienteRecuperado.hematocrito - 0.1);
                }
            },
            aumentarVCM() {
                this.pacienteRecuperado.vcm = this.corrigirCasasDecimais(this.pacienteRecuperado.vcm + 0.1);
            },
            diminuirVCM() {
                if (this.pacienteRecuperado.vcm > 0) {
                    this.pacienteRecuperado.vcm = this.corrigirCasasDecimais(this.pacienteRecuperado.vcm - 0.1);
                }
            },
            aumentarHCM() {
                this.pacienteRecuperado.hcm = this.corrigirCasasDecimais(this.pacienteRecuperado.hcm + 0.1);
            },
            diminuirHCM() {
                if (this.pacienteRecuperado.hcm > 0) {
                    this.pacienteRecuperado.hcm = this.corrigirCasasDecimais(this.pacienteRecuperado.hcm - 0.1);
                }
            },
            aumentarCHCM() {
                this.pacienteRecuperado.chcm = this.corrigirCasasDecimais(this.pacienteRecuperado.chcm + 0.1);
            },
            diminuirCHCM() {
                if (this.pacienteRecuperado.chcm > 0) {
                    this.pacienteRecuperado.chcm = this.corrigirCasasDecimais(this.pacienteRecuperado.chcm - 0.1);
                }
            },
            aumentarRDW() {
                this.pacienteRecuperado.rdw = this.corrigirCasasDecimais(this.pacienteRecuperado.rdw + 0.1);
            },
            diminuirRDW() {
                if (this.pacienteRecuperado.rdw > 0) {
                    this.pacienteRecuperado.rdw = this.corrigirCasasDecimais(this.pacienteRecuperado.rdw - 0.1);
                }
            },
            corrigirCasasDecimais(valor) {
                return Math.round(valor * 100) / 100;
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
