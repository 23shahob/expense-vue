<script setup>
const {total,income,expense} = defineProps({
    total: {
        type: Number,
        required: true
    },income: {
        type: Number,
        required: true
    },expense: {
        type: Number,
        required: true
    }
})
</script>

<template>
    <div class="balance">
        <header>
            <h3>YOUR BALANCE</h3>
            <h3>${{total}}</h3>
        </header>
        <div class="balance-wrapper">
            <div>
                <h3>INCOME</h3>
                <h3 class="income-text">+${{income}}</h3>
            </div>
            <div class="line"></div>
            <div>
                <h3>EXPENSE</h3>
                <h3 class="expense-text">-${{-  expense}}</h3>
            </div>
        </div>
    </div>
</template>
<style scoped>
header {
    margin-bottom: 16px;
}

header h3:first-child {
    font-weight: 400;
    margin-bottom: 4px;
}

.balance-wrapper {
    display: flex;
    justify-content: space-evenly;
        padding: 16px;
    background-color: #fff;
    box-shadow: 4px 4px 12px darkgray;
}
.line{
    border: 1px solid gray;
}

.balance-wrapper div {
    display: flex;
    flex-direction: column;
    gap: 6px;
}

.balance-wrapper h3 {
    font-weight: 400;
}

.income-text {
    color: forestgreen;
}

.expense-text {
    color: brown;
}
</style>