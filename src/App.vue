<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionsList />
    <AddTransaction />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionsList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

export default {
  components: {
    Header,
    Balance,
    IncomeExpenses,
    TransactionsList,
    AddTransaction,
  },
};
</script>
