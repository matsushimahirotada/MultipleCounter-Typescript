<script lang="ts">
  import { fade } from "svelte/transition";
</script>

<div class="box" transition:fade>
  <slot />
</div>

<style>
  .box {
    filter: brightness(1.1);
    background-color: rgba(180, 180, 180, 0.349);
    width: 480px;
    border: 1px solid #aaa;
    border-radius: 2px;
    box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
    padding: 1em;
    margin: 0 0 1em 0;
  }
</style>
