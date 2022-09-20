<script>
  import { fade, slide } from "svelte/transition";
</script>

<div class="modal-container" transition:fade>
  <div class="modal-content">
    <slot />
  </div>
</div>
