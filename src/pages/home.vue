<template>
    <div>
        <span class="back"  @click="goBack">
            <i class="icon icon-back"></i>
            <home-swiper></home-swiper>
                首页 {{my.pageSize}} 
        </span>
        <input type="text" v-model="todoValue">
        <button @click="hand">提交</button>
        <hello-world 
            v-for="(item,index) in list" 
            v-bind:content='item'
            v-bind:key="index"
            v-bind:index="index"
            @delete="handledetele">
         </hello-world>
    </div>
</template>
<script>
// 父组件通过 v-bind:content（:content）向子组件传值，子组件得从props接收
// 子组件通过$emit()事件向上一层触发事件，父组件在监听
import helloWorld from '../components/HelloWorld'
import HomeSwiper from '../components/swiper'
import Axios from 'axios'
export default {
    data() {
        return {
            my: {},
            list: [],
            todoValue: ''
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
        },
        hand() {
            this.list.push(this.todoValue)
            this.todoValue = ''
        },
        handledetele(index) {
            this.list.splice(index, 1)
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
