<script setup>
    import {ref, defineEmits} from 'vue'
    
    const text = ref('')
    const amount = ref('')
    const calories = ref('')

    const emit = defineEmits([
        'transactionSubmitted'
    ])
    const onSubmit = () =>{
        const transactionData = {
            text: text.value,
            amount: parseFloat(amount.value),
            calories: parseFloat(calories.value),
        }

        emit('transactionSubmitted', transactionData)

        text.value = ''
        amount.value = ''
        calories.value = ''
    }
</script>

<template>
    <h3>Add a new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Enter Item</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Item..."/>
        </div>
        <div class="form-control">
            <label for="amount">Enter Cost</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter Negative Value for Discounts"/>
        </div>
        <div class="form-control">
            <label for="calories">Enter Number of Calories</label>
            <input type="text" id="calories" v-model="calories" placeholder="Enter calorie amount"/>
        </div>
        <button class="btn">Add Item</button>


    </form>
</template>