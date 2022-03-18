<script lang="ts">
  export let align: string = "center";
  export let justify: string = "center";
  export let gap: string = "0";
</script>

<div
  class="row"
  style="
    align-items: {align};
    justify-content:{justify};
    gap:{gap}
  "
>
  <slot />
</div>

<style>
  .row {
    display: flex;

    width: 100%;
  }
</style>
