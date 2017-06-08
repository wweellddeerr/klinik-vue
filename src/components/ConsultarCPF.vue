<template>
    <div class="row">
        <div class="col-xs-offset-4 col-xs-4">
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
                        this.resultadoFn(response.data);
                    }
                 );

            }
        },
        watch: {
            cpf() {
                while(this.cpf.length > 0 && isNaN(this.cpf)) {
                    this.cpf = this.cpf.substring(0, this.cpf.length - 1);
                }

                if(this.cpf.length === 11) {
                    this.cpfInformado = true;
                    this.consultarCPF();
                }

            }
        }
    }
</script>

<style>

</style>