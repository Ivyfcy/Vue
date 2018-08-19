<template>
    <div>
        <span class="back"  @click="goBack">
            <i class="icon icon-back"></i>
            <home-swiper></home-swiper>
                首页 {{my.pageSize}} 
        </span>
        <div @click="changecolor" :class="{active:isactive}" v-if="show">{{message}}</div>
        <div>{{ full}}</div>
        <input type="text" v-model="todoValue">
        <button @click="hand">提交{{conpulate}}</button>
        <hello-world 
            v-for="(item,index) in list" 
            v-bind:content='item'
            :key="index"
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
    // list列表渲染对数据操作下标不会改变页面的渲染
    // 利用push pop shift unshift splice sort reverse方法来改变
    data() {
        return {
            my: {},
            list: [],
            todoValue: '',
            first: 'fcy',
            last: 'ivy',
            isactive: false,
            message: 'hello word',
            show: false
        }
    },
    // 监听，和计算属性一样有缓存机制，但是代码比较复杂，建议优选使用计算属性
    // watch: {
    //     first() {
    //         this.full = this.first + this.last
    //     },
    //     last() {
    //         this.full = this.first + this.last
    //     }
    // },
    // 计算属性，有个缓存机制，只要不改变相关的计算值就不会重新计算
    computed: {
        conpulate() {
            return this.first + this.last
        },
        full: {
            get() {
                return this.first + ' ' + this.last
            },
            set(value) {
                let arr = value.split(' ')
                this.first = arr[0]
                this.last = arr[1]
                console.log(99999, value)
            }
        }
    },
    // 生命周期函数就是vue实例在某一个时间点会自动执行得函数8 11
    beforeCreate() {
        console.log('beforecreate')
    },
    created() {
        console.log('creat')
    },
    beforeMount() {
        console.log('beforeMount', this.$el)
    },
    mounted() {
        const self = this
        Axios.get('/api/posts').then(data => {
            self.my = data.data
        })
        console.log(this.$el)
    },
    beforeDestroy() {
        console.log('beforeDestroy')
    },
    destroy() {
        console.log('destroy')
    },
    beforeUpdate() {
        console.log('beforeUpdate')
    },
    updated() {
        console.log('Update')
    },
    methods: {
        goBack() {
            console.log('点击首页')
        },
        hand() {
            this.show = true
            this.full = 'ttt 000'
            this.list.push(this.todoValue)
            this.todoValue = ''
        },
        handledetele(index) {
            this.list.splice(index, 1)
        },
        changecolor() {
            this.isactive = !this.isactive
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
.active{
    color: red
}
</style>
