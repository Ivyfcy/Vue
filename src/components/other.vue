<template>
  <div>
    <span class="back" @click="goBack">
      <i class="icon icon-back"></i>
      <router-link :to="{ name: 'home' }">返回</router-link>
    </span>
  </div>
</template>
<script>
export default {
    name: 'other',
    methods: {
        goBack() {
            console.log('返回')
        }
    }
}
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
