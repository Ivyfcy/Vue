<template>
    <div>
        <span class="back"  @click="goBack">
            <i class="icon icon-back"></i>
            <home-swiper></home-swiper>
            <div>首页 {{my.pageSize}} </div>
        </span>
        <hello-world></hello-world>
    </div>
</template>
<script>
import helloWorld from '../components/HelloWorld'
import HomeSwiper from '../components/swiper'
import Axios from 'axios'
export default {
    data() {
        return {
            my: {}
        }
    },
    mounted() {
        const self = this
        Axios.get('/api/posts').then(data => {
            self.my = data.data
        })
    },
    methods: {
        goBack() {
            console.log('点击首页')
        }
    },
    components: {
        helloWorld,
        HomeSwiper
    }
}
</script>

<style scoped>
a {
  color: #42b983
}
</style>
