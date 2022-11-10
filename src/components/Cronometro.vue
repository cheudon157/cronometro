<template>
    <div>

        <div class="row  justify-content-center mt-2">
            <h1><span class="text-gradient">Cronomêtro</span></h1>
        </div>

        <div class="row justify-content-center mt-2">
            <input type="date" v-model="data" @change.prevent="contagemRegressiva()">
        </div>

        <div class="row row justify-content-center mt-2">
            <div class="col-sm-12 col-md-3 col-lg-3  mt-2">
                <div class="alert alert-success" role="alert">
                    <h4 class="alert-heading"> Dias {{ dia }}</h4>
                </div>
                <div class="progress">
                    <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar"
                        aria-valuenow="0" aria-valuemin="0" aria-valuemax="60"
                        :class="barraProgresso(((dia / 30) * 100))" :style="{ 'width': ((dia / 30) * 100) + '%' }">
                    </div>
                </div>
            </div>
            <div class="col-sm-12 col-md-3 col-lg-3  mt-2">
                <div class="alert alert-success" role="alert">
                    <h4 class="alert-heading"> Horas {{ horas }}</h4>
                </div>
                <div class="progress">
                    <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar"
                        aria-valuenow="0" aria-valuemin="0" aria-valuemax="60"
                        :class="barraProgresso(((horas / 24) * 100))" :style="{ 'width': ((horas / 24) * 100) + '%' }">
                    </div>
                </div>
            </div>
            <div class="col-sm-12 col-md-3 col-lg-3  mt-2">
                <div class="alert alert-success" role="alert">
                    <h4 class="alert-heading"> Minutos {{ minutos }}</h4>
                </div>
                <div class="progress">
                    <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar"
                        aria-valuenow="0" aria-valuemin="0" aria-valuemax="60"
                        :class="barraProgresso(((minutos / 60) * 100))"
                        :style="{ 'width': ((minutos / 60) * 100) + '%' }"></div>
                </div>
            </div>
            <div class="col-sm-12 col-md-3 col-lg-3  mt-2">
                <div class="alert alert-success" role="alert">
                    <h4 class="alert-heading"> Segundos {{ segundos }}</h4>
                </div>
                <div class="progress">
                    <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar"
                        aria-valuenow="0" aria-valuemin="0" aria-valuemax="60"
                        :class="barraProgresso(((segundos / 60) * 100))"
                        :style="{ 'width': ((segundos / 60) * 100) + '%' }"></div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>

import moment from 'moment'
export default {
    data() {
        return {
            data: '',
            dia: 0,
            horas: 0,
            minutos: 0,
            segundos: 0,
        }
    },
    methods: {
        contagemRegressiva() {

            let diferenca = moment(this.data).format('x') - moment().format('x')

            if (diferenca > 0) {
                setTimeout(() => {

                    this.dia = Math.floor((diferenca / (1000 * 60 * 60 * 24)));
                    this.horas = Math.floor((diferenca % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                    this.minutos = Math.floor((diferenca % (1000 * 60 * 60)) / (1000 * 60));
                    this.segundos = Math.floor((diferenca % (1000 * 60)) / 1000);
                    this.contagemRegressiva()

                }, 1000)
            } else {
                this.dia = 0;
                this.horas = 0;
                this.minutos = 0;
                this.segundos = 0;
            }

        },
        barraProgresso(valor) {
            if (valor < 33) {
                return 'bg-danger'
            } else if (valor < 66) {
                return 'bg-warning'
            } else {
                return 'bg-success'
            }
        }

    }
}
</script>

<style scoped>
.text-gradient {
    background-image: var(--accent-gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-size: 400%;
    background-position: 0%;
}
</style>
