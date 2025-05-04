<script setup>
import Balance from "./components/Balance.vue";
import TransactionList from "./components/TransactionList.vue"
import TransactionForm from "./components/TransactionForm.vue"
import { computed, onMounted, ref } from "vue";
import { useToast } from "vue-toastification";


const transactions = ref([
  
]);

onMounted(() => {
  const storedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if (storedTransactions) {
    transactions.value = storedTransactions;
  }
});

const total= computed(()=>{
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
})
const income= computed(()=>{
  return transactions.value.filter(transaction => transaction.amount > 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
})
const expense= computed(()=>{
  return transactions.value.filter((transaction) => transaction.amount < 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
})

const handleSubmit = (transactionData) => {
  console.log(transactionData);
  transactions.value.push(transactionData);
  saveTransactions();
  useToast().success("Transaction added successfully");
};

const handleDelete = (id) => {
  transactions.value = transactions.value.filter((transaction)=> transaction.id !== id)
  saveTransactions();
  useToast().success("Transaction deleted successfully");
};

const saveTransactions = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
}
</script>
<template>
  <div id="container">
    <header>
      <h1>Expense Tracker</h1>
    </header>
    <Balance :total="+total" :income="+income" :expense="+expense"/>
    <TransactionList :transactions="transactions" @deleteTransaction="handleDelete"/>
    <TransactionForm @addTransaction="handleSubmit"/>
  </div>
</template>
<style scoped>
#container {
  width: 100%;
  max-width: 400px;
  display: flex;
  flex-direction: column;
  gap: 25px;
  color: #2a2929;
}

header h1 {
  font-weight: 500;
}
</style>