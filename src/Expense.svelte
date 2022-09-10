<script>
  export let name = "",
    amount = 0,
    id;
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn">
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    <h4>amount :${amount}</h4>
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn">
        <div class="fas fa-pen"></div>
    </button>
    <button class="expense-btn delete-btn">
      <div class="fas fa-trash"></div>
  </button>
  </div>
</article>
