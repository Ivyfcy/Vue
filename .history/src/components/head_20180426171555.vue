<template>
    <header>
        <span class="back" @click="goBack">
            <i class="icon icon-back"></i>
            返回
        </span>
    </header>
</template>
<script>
export default {
  methods: {
    goBack () {
      console.log(2222)
    }
  }
}
</script>
