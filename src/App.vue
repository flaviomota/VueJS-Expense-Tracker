<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionsList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionsList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 },
]);

// Get Total
const total = computed(() => {
  return transactions.value.reduce((accumulator, transaction) => {
    return accumulator + transaction.amount;
  }, 0);
});

//Get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Get Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0)
    .toFixed(2);
});

// Add Transaction
const handleTransactionSubmitted = (transactionData) => {
  //console.log(transactionData);

  transactions.value.push({
    id: generateUniqueID(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  //console.log(generateUniqueID());
  toast.success('Transaction added');
};

// Generate Unique ID
const generateUniqueID = () => {
  return Math.floor(Math.random() * 1000000);
};

// Delete Transaction
const handleTransactionDeleted = (id) => {
  //console.log(id);

  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  toast.success('Transaction deleted!');
};
</script>
