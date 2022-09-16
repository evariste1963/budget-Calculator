<script>
  import { getContext } from "svelte";
  import { slide } from "svelte/transition";
  export let name = "",
    amount = 0,
    id;

  let displayAmount = false;
  const toggleAmount = () => {
    displayAmount = !displayAmount;
  };
  const removeExpense = getContext("remove");
  const setModifiedExpense = getContext("modify");
</script>

<article class="single-expense" transition:slide>
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={toggleAmount}>
        {#if !displayAmount}
          <i class="fas fa-caret-down" />
        {:else}
          <i class="fas fa-caret-up" />
        {/if}
      </button>
    </h2>
    {#if displayAmount}
      <h4 transition:slide>amount :£{amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button
      class="expense-btn edit-btn"
      on:click={() => {
        setModifiedExpense(id);
      }}
    >
      <div class="fas fa-pen" />
    </button>
    <button
      class="expense-btn delete-btn"
      on:click={() => {
        removeExpense(id), (displayAmount = false);
      }}
    >
      <div class="fas fa-trash" />
    </button>
  </div>
</article>
