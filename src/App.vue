<template>
    <div class="container grid-lg my-2 py-2">
        <div class="card">
            <div class="card-header">
                <div class="h4">Todas as Moedas</div>
            </div>
            <div class="card-body">
                <ListQuotes :quotes="quotes"/>
            </div>
        </div>
    </div>
</template>

<script>

import {onMounted, reactive, toRefs} from 'vue'
import api from '@/services/api'
import ListQuotes from './components/ListQuotes.vue'

export default {
    name: 'App',
    components:{
        ListQuotes
    },
    setup(){
        // const model = ref('Hello World')
        // model.value = 'Qualquer coisa'

        const data = reactive({
            quotes:{},
        })

        onMounted(async() =>{
            const response = await api.all()
            data.quotes = response.data
        })

        api.all().then(response=>{
            data.quotes = response.data
        })

        // return {model}
        return {...toRefs(data)}
    }

}
</script>

