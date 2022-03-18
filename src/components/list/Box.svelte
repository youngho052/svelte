<script>
</script>

<div class="listItem" on:click>
  <slot />
</div>

<style>
  .listItem {
    display: flex;
    justify-content: space-between;
    width: 50%;
    padding: 20px;
    border: 1px solid #000;
  }
</style>
