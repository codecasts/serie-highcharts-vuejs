
<script>

    import Highcharts from 'highcharts'
    import base from './base.vue'
    import _ from 'lodash'
    export default {
        extends: base,
        methods: {
            /**
            * Utilizado para ler a lista e calcular a fonte de dados do grafico
            */
            dataSource() {

                const countries = this.localList.map(item => item.country)

                const base = _(countries)
                    .countBy()
                    .map((value, key) => ({ key, value }))
                    .orderBy(['value'], ['desc'])
                    .value()

                const categories = base.map(item => item.key)

                const values = base.map(item => item.value)

                if (this.chart === null) {
                    this.chart = this.setup({ categories, values })
                } else {
                    this.chart.series[0].setData(values)
                }
            },

            /**
            * Para montar o grafico e exibi-lo na tela.
            * Obs: este metodo só poderá ser chamado quando a fonte de dados
            * estiver pronta
            */
            setup(obj) {
                const { categories, values } = obj
                return Highcharts.chart('container-for-countries', {
                    chart: {
                        type: 'column'
                    },
                    title: {
                        text: 'Countries'
                    },
                    subtitle: {
                        text: 'Source: codecasts.com.br'
                    },
                    xAxis: {
                        categories: categories,
                        crosshair: true
                    },
                    yAxis: {
                        min: 0,
                        title: {
                            text: 'Quantidade'
                        }
                    },
                    series: [{
                        name: 'Quantidade',
                        data: values
                    }]
                });
            },
        },
    }
</script>

<template>
    <div id="container-for-countries"></div>
</template>