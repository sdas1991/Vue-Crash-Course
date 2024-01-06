<template>
    <button @click="onClick()" :style="{ background: color}" class="btn">{{  text }}</button>
</template>

<script>
export default {
    name:'ButtonHeader',
    props: {
        text: String,
        color: String
    },
    methods: {
        onClick() {
        this.$emit('toggle-add-task')
    }
},
emits: ['toggle-add-task'],
}
</script>