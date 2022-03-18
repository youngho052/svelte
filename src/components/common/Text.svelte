<script lang="ts">
  export let size: string = "14px";
  export let color: string = "#000";
</script>

<div
  class="text"
  on:click
  style="
    font-size:{size};
    color: {color};
  "
>
  <slot />
</div>
