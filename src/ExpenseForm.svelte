<script>
  import Title from "./Title.svelte";
  export let addExpense;
  export let name = "";
  export let amount = null;
  export let isEditing;
  export let editExpense;

  $: isEmpty = !name || !amount;

  function handleSubmit() {
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      addExpense({ name, amount });
    }
    name = "";
    amount = null;
  }

  //workaround that makes FOCUS work all the time.
  function autoFocus(el) {
    setTimeout(() => {
      el.focus();
    }, 100);
  }
</script>

<section class="form">
  <Title title="add expense" />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" id="name" bind:value={name} use:autoFocus />
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">please fill out all form fields</p>
    {:else}
      <p />
      <br />
    {/if}

    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}>{isEditing ? "amend expense" : "add expense"}</button
    >
    <button type="button" class="close-btn" on:click
      ><i class="fas fa-times" />close</button
    >
  </form>
</section>
