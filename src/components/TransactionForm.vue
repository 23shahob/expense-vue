<script setup>
import { onMounted, ref } from "vue";
import { useToast } from "vue-toastification";  
const text = ref("");
const amount = ref("");
const emit = defineEmits(["addTransaction"]);

const onsubmit = ()=>{
    if (!text.value || !amount.value) {
        useToast().error("Please fill in all fields");
        return;
    }
    const transactionData = {
        id: Date.now(),
        text: text.value,
        amount: Number(amount.value),
    };
    emit("addTransaction", transactionData); 
    text.value = "";
    amount.value = "";
}
</script>

<template>
  <div class="form">
    <header>
      <h3>Add new transaction</h3>
    </header>
    <form id="form" @submit.prevent="onsubmit">
      <div><label for="text">Text</label> <input v-model="text" class="field" type="text" id="text" placeholder="Enter text..."/></div>
      <div>
        <label for="amount">Amount</label> <input v-model="amount" class="field" type="text" id="amount" placeholder="Enter amount..."/>
      </div>
      <button class="field" >Add transaction</button>
    </form>
  </div>
</template>
<style scoped>
header {
  padding-bottom: 12px;
  border-bottom: 1px solid darkgray;
}
header h3 {
  font-weight: 500;
}
form {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 16px 0;
}
form div{
    display: flex;
    flex-direction: column;
    gap: 8px;
}
.field{
    padding: 8px 14px;
    font-size: 16px;
    border-radius: 4px;
}
input{
    border: 1px solid gray;
}
input:focus {
    outline-color: darkviolet;
    border-color: darkviolet;
}

input:active {
    border-color: darkviolet; 
}
button {
    background-color: darkviolet;
    color: white;
    border: none;
    padding: 10px 16px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: darkviolet;
}

button:active {
    background-color: rgdarkviolet;
}

button:disabled {
    background-color: lightgray;
    cursor: not-allowed;
}
</style>
