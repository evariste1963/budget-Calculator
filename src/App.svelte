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
  let isFormOpen = false;
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
  }

  function openForm() {
    isFormOpen = true;
  }

  function closeForm() {
    isFormOpen = false;
  }

  //context
  setContext("remove", removeExpense);
</script>

<Navbar on:click={openForm} />
<main class="content">
  {#if isFormOpen}
    <ExpenseForm on:click={closeForm} {addExpense} />
  {/if}
  <Totals title="total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
  {#if expenses.length > 0}
    <Button on:click={clearExpenses} label="clear expenses" />
  {/if}
</main>

<style>
</style>
