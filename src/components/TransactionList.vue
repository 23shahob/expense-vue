<script setup>
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
})
const emit = defineEmits(["deleteTransaction"]);

const deleteTransaction = (id)=>{
    emit("deleteTransaction", id);
}
</script>
<template>
    <div class="history">
        <header>
            <h3>History</h3>
        </header>
        <ul class="list">
            <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
                <p>{{ transaction.text }}</p><span>${{ transaction.amount }}</span>
                <button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
            </li>

        </ul>
    </div>
</template>
<style scoped>
header{
    padding-bottom: 12px;
    border-bottom: 1px solid darkgray;
}
header h3 {
    font-weight: 500;
}
.list{
    display: flex;
    flex-direction: column;
    gap: 12px;
    padding: 16px 0;
}
.list li{
    display: flex;
    justify-content: space-between;
    padding: 10px 12px;
    box-shadow: 2px 2px 4px darkgray;
    position: relative;
}
li.minus{
border-right: 4px solid brown;
}
li.plus{
    border-right: 4px solid forestgreen;
}
.delete-btn{
    display: none;
    /* position: absolute; */
    /* right: 10px; */
    /* top: 50%; */
    /* transform: translateY(-50%); */
    background-color: crimson;
    color: white;
    border: none;
    border-radius: 50%;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
    width: 20px;
    height: 20px;
    text-align: center;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
}

.delete-btn:hover {
    background-color: darkred;
    /* transform: translateY(-50%) scale(1.1); */
}

.delete-btn:active {
    background-color: firebrick;
    /* transform: translateY(-50%) scale(0.95); */
}
li:hover span{
    display: none;
}
li:hover .delete-btn {
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>