<script>
  import SectionTitle from "./Title.svelte";
  import Expense from "./Expense.svelte";
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";

  export let expenses = [];
  customElements.define(
    "delayed-content",
    class extends HTMLElement {
      connectedCallback() {
        setTimeout(() => {
          this.removeAttribute("hidden");
        }, Number(this.getAttribute("delay")));
      }
    }
  );
</script>

<section>
  <SectionTitle title="expense list" />
  <ul>
    {#each expenses as expense, index (expense.id)}
      <div
        in:fly={{ x: -200, delay: (index + 1) * 700, duration: 1500 }}
        animate:flip={{ duration: 1000 }}
      >
        <Expense {...expense} />
      </div>
    {:else}
      <delayed-content delay="500" hidden>
        <h2>no expenses added to the list</h2>
      </delayed-content>
    {/each}
  </ul>
</section>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
