<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        amount: {
            type: Number,
            require: true,     
        }
    })
</script>
<template>
    <h1 id="balance">{{ amount }}</h1>
</template>