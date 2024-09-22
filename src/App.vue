<script setup>
  import Header from './components/Header.vue';
  import TotalBalance from './components/TotalBalance.vue';
  import ItemsDiscounts from './components/ItemsDiscounts.vue';
  import AddGroceryItem from './components/AddGroceryItem.vue';
  import GroceryList from './components/GroceryList.vue';

  import {ref, computed, onMounted} from 'vue'

  const transactions = ref([
  ])

  const calcSub = computed(()=>{
    return transactions.value.reduce((acc, x)=>{
      return acc+x.amount
    },0)
  })

  const calcTax = computed(()=>{
    return transactions.value.reduce((acc, x)=>{
      return (acc+x.amount*0.0825).toFixed(3)
    },0)
  })

  const calcTot = computed(()=>{
    return transactions.value.reduce((acc, x)=>{
      return (acc+x.amount*1.0825).toFixed(2)
    },0)
  })

  const moneyIn = computed(()=>{
    return transactions.value
    .filter((x)=>x.amount>0)
    .reduce((acc, x)=>{
      return acc+x.amount
    },0)
  })
  const moneyOut = computed(()=>{
    return transactions.value
    .filter((x)=>x.amount<0)
    .reduce((acc, x)=>{
      return acc+x.amount
    },0)
  })

  const handleTransaction = (transactionData) => {
    transactions.value.push({
      id: generateID(),
      text: transactionData.text,
      amount: transactionData.amount,
      calories: transactionData.calories,
    })
    saveToLocalStorage()
  }

  const generateID = () =>{
    return Math.floor(Math.random()*10000000)
  }

  const handleDelete = (id) =>  {
    transactions.value = transactions.value.filter((x) => x.id !== id)
    saveToLocalStorage()
  }

  const saveToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
  }

  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'))

    if(savedTransactions){
      transactions.value = savedTransactions
    }
  })
</script>

<template>
    <Header></Header>
    <div class="container">
      <ItemsDiscounts :income="moneyIn" :expense="moneyOut"></ItemsDiscounts>
      <AddGroceryItem @transactionSubmitted="handleTransaction"></AddGroceryItem>
      <GroceryList :transactions="transactions" @transactionDeleted="handleDelete"></GroceryList>
      <h4>Total Amounts</h4>
      <label>Subtotal</label>
      <TotalBalance :amount="calcSub"></TotalBalance>
      <label>Tax</label>
      <TotalBalance :amount="calcTax"></TotalBalance>
      <label>Total</label>
      <TotalBalance :amount="calcTot"></TotalBalance>
    </div>
</template>