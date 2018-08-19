<template>
    <div>
        <span class="back"  @click="goBack">
            <i class="icon icon-back"></i>
            <home-swiper></home-swiper>
                首页 {{my.pageSize}} 
        </span>
        <div @click="changecolor" 
        :class="{active:isactive}" 
        v-if="show"
        ref="a"
        >{{message}}
        </div>
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
         <counter @numberchange="addnumber" ref="one"></counter>
         <counter @numberchange="addnumber" ref="two"></counter>
         <div>{{numbertall}}</div>
    </div>
</template>
<script>
// 父组件通过 v-bind:content（:content）向子组件传值，子组件得从props接收
// 子组件通过$emit()事件向上一层触发事件，父组件在监听
import helloWorld from '../components/HelloWorld'
import HomeSwiper from '../components/swiper'
import counter from '../components/counter'
import Axios from 'axios'
export default {
    // list数组列表渲染如果对数据下标进行操作改变数据但不会改变页面的渲染，但其实数据已经改变
    // 1.利用push pop shift unshift splice sort reverse方法来改变，2.也可以通过改变数据的引用
    // 3.
    data() {
        return {
            my: {},
            list: [],
            todoValue: '',
            first: 'fcy',
            last: 'ivy',
            isactive: false,
            message: 'hello word',
            show: false,
            numbertall: 0
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
            // set方法  没法使用识别vue
            // Vue.set(this.list, 1, 5)
            this.todoValue = ''
        },
        handledetele(index) {
            this.list.splice(index, 1)
        },
        changecolor() {
            this.isactive = !this.isactive
            // ref写在div等标签里，是通过this.$refs.name获取dom节点
            console.log(this.$refs.a.innerHTML)
        },
        addnumber() {
            // ref写在子组件里，通过this.$refs.name获取子组件的引用
            this.numbertall = this.$refs.one.number + this.$refs.two.number
        }
    },
    components: {
        helloWorld,
        HomeSwiper,
        counter
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
