<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <router-link :to="{ name: 'other' }">下个页面</router-link>
    <li @click="handledelete">{{content}}</li>
  </div>
</template>

<script>
export default {
    props: {
        content: {
            type: String,
            required: true, // 必传
            // 自定义校验器
            validator(value) {
                return (value.length > 5)
            }

        },
        index: {
            type: Number
        }
    },
    name: 'HelloWorld',
    data() {
        return {
            msg: 'Welcome to  Vue'
        }
    },
    methods: {
        handledelete() {
            this.$emit('delete', this.index)
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
a {
  color: #42b983;
}
</style>
