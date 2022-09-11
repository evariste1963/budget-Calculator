<script>
  export let name = "",
    amount = 0,
    id;
  let displayAmount = false;

  const toggleAmount = () => {
    displayAmount = !displayAmount;
  };
</script>

<article class="single-expense">
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
      <h4>amount :${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn">
      <div class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn">
      <div class="fas fa-trash" />
    </button>
  </div>
</article>
