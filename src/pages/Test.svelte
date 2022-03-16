<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let name: string = "parkpark";
  export let border: string = "1px solid blue";

  const testclick = () => {
    dispatch("message", {
      text: name,
    });
  };
</script>

<p on:click="{testclick}" style="---border:{border}">name is {name}</p>

<style>
  p {
    border: var(---border);
    color: blue;
  }
</style>
