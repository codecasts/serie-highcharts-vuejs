
<script>
    import filters from './filters.vue'
    import countries from './charts/countries.vue'
    import languages from './charts/languages.vue'
    import axios from 'axios'

    const http = axios.create()

    export default {
        components: {
            filters, countries, languages
        },
        mounted() {
            http.get('/MOCK_DATA.json').then(response => {
                this.$store.commit('SET_LIST', response.data)
            })
        },
    }
</script>

<template>
    <div class="container">
        <div class="well">
            <filters></filters>
        </div>
        <div class="row">
            <div class="col-md-6">
                <countries></countries>
            </div>
            <div class="col-md-6">
                <languages></languages>
            </div>
        </div>
    </div>
</template>