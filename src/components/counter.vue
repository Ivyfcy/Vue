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
            this.number = this.number + 2
            this.$emit('numberchange', 2)
        }
    }
}
</script>
