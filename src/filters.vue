
<script>
    export default {
        data() {
            return {
                gender: ''
            }
        },
        methods: {
            commit() {
              this.$store.commit('SET_FILTER', this.gender)
            },
        },
    }
</script>

<template>
    <div>
        <select @change="commit" v-model="gender">
            <option value="">Ambos</option>
            <option value="Male">Homens</option>
            <option value="Female">Mulheres</option>
        </select>
    </div>
</template>