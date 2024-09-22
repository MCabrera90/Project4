<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        subTotal: {
            type: Number,
            require: true,   
        },
        tax: {
            type: Number,
            require: true,   
        },
        total: {
            type: Number,
            require: true,     
        }
    })
</script>
<template>
    <h4>SubTotal</h4>
    <h1 id="balance">{{ subTotal }}</h1>
    <h4>Tax</h4>
    <h1 id="balance">{{ tax }}</h1>
    <h4>Total</h4>
    <h1 id="balance">{{ total }}</h1>
</template>