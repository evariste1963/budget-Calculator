<script>
  // https://www.youtube.com/watch?v=uk1eM0Yn0UQ

  import { setContext } from "svelte";

  //components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  //data
  import expensesData from "./expenses";

  //variables
  let expenses = [...expensesData];

  //functions
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }

  function clearExpenses() {
    expenses = [];
  }
  //context
  setContext("remove", removeExpense);
</script>

<Navbar />

<main class="content">
  <ExpensesList {expenses} />
  {#if expenses.length > 0}
    <button
      type="button"
      class="btn btn-primary btn-block"
      on:click={clearExpenses}>clear expenses</button
    >
  {/if}
</main>

<style>
</style>
