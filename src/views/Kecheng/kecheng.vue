<template>
    <div>
        <kecheng-list :kechengs="kechengs"></kecheng-list>                          
    </div>
</template>

<script>
import KechengList from './kecheng_list'
import axios from 'axios'
import { Message } from 'element-ui';
export default {
    name:'kecheng',
    components: {
        KechengList
    },
    data () {
        return {
            kechengs:[],
        }
    },
    methods: {
        getKechengList(){
            axios.get('http://www.hhfff.cn/api/kechengs')
            .then((res)=>{
                let data = res.data
                if (data.code != '000') {
                    Message.success('暂时没有课程，请尽情期待！') 
                } else if (data.code == '000') {
                    this.kechengs = data.data
                } 
            })
            .catch((error)=>{
               console.log(error)
               Message.error('暂时没有课程，请尽情期待！') 
            })
        }
    },
    mounted () {
        this.getKechengList()
    }
}
</script>

