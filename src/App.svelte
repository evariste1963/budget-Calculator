<script>
  // https://www.youtube.com/watch?v=uk1eM0Yn0UQ
  //components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  //data
  import expensesData from "./expenses";

  //variables
  let expenses = [...expensesData];
</script>

<Navbar />

<main class="content">
  <ExpensesList {expenses} />
</main>

<style>
</style>
