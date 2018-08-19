<template>
    <div @click="handleclick">
        {{number}}
    </div>
</template>
<script>
export default {
    name: 'counter',
    data() {
        return {
            number: 0
        }
    },
    methods: {
        handleclick() {
            this.number++
            this.$emit('numberchange')
        }
    }
}
</script>
