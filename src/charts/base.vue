
<script>
    import { mapState } from 'vuex'
    export default {
        computed: {
            ...mapState({
                list: state => state.list,
                filter: state => state.filter,
            }),
            localList() {
                let list = this.list
                if (this.filter !== '') {
                    list = list.filter(item => item.gender === this.filter)
                }
                return list
            }
        },
        watch: {
            list() {
                this.dataSource()
            },
            filter() {
                this.dataSource()
            },
        },
        data() {
          return {
            chart: null
          }
        },
    }
</script>