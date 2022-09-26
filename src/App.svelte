<script>
  // https://www.youtube.com/watch?v=uk1eM0Yn0UQ
  import {
    setContext,
    onMount,
    onDestroy,
    beforeUpdate,
    afterUpdate,
  } from "svelte";
  //components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Button from "./Button.svelte";
  //data
  //import expensesData from "./expenses";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Modal from "./Modal.svelte";

  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });

  //after update --> runs EVERY time the app does anything, so not always the best place to update this as it may slow things down if egtting form an API ect --> maybe better to call setLocoalStorage everytime it's actually necessary
  afterUpdate(() => {
    setLocalStorage();
  });

  //variables
  let expenses = [];
  let isFormOpen = false;
  //set editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  //reactive variables
  $: isEditing = setId ? true : false;
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
    closeForm();
  }

  function openForm() {
    isFormOpen = true;
  }

  function closeForm() {
    isFormOpen = false;
    setId = null;
    setName = "";
    setAmount = null;
    isEditing = false;
  }

  function setModifiedExpense(id) {
    openForm();
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
  }

  function editExpense({ name, amount }) {
    expenses = expenses.map(item => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setAmount = null;
    setName = "";
    closeForm();
  }
  //context
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);

  //local Storage
  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }
</script>

<Navbar on:click={openForm} />
<main class="content">
  {#if isFormOpen}
    <Modal>
      <ExpenseForm
        on:click={closeForm}
        {addExpense}
        name={setName}
        amount={setAmount}
        {isEditing}
        {editExpense}
      />
    </Modal>
  {/if}

  <Totals title="total Expenses" {totalExpenses} />

  <ExpensesList {expenses} />

  {#if expenses.length > 0}
    <Button on:click={clearExpenses} label="clear expenses" />
  {/if}
</main>

<style>
</style>
