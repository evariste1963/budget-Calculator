<script>
  // https://www.youtube.com/watch?v=uk1eM0Yn0UQ

  import { setContext } from "svelte";

  //components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Button from "./Button.svelte";
  //data
  import expensesData from "./expenses";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";

  //variables
  let expenses = [...expensesData];

  //reactive variables
  $: totalExpenses = expenses.reduce((acc, cur) => (acc += cur.amount), 0);

  //functions
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }

  function clearExpenses() {
    expenses = [];
  }

  function addExpense({ name, amount }) {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
    console.log(name, amount);
  }

  //context
  setContext("remove", removeExpense);
</script>

<Navbar />

<main class="content">
  <ExpenseForm {addExpense} />
  <Totals title="total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
  {#if expenses.length > 0}
    <Button on:click={clearExpenses} label="clear expenses" />
  {/if}
</main>

<style>
</style>
