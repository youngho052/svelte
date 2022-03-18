<script lang="ts">
  import { useParams } from "svelte-navigator";
  import { createEventDispatcher, onMount } from "svelte";
  import axios from "axios";
  import { API } from "../api/api";

  const params = useParams();

  let detailData: any[] = [];

  const init = async () => {
    try {
      const response = await axios.get(`${API}/example/${$params.id}`);

      detailData = response.data.data.Items;
    } catch (error) {
      console.log(error);
    }
  };

  onMount(() => {
    init();
  });

  const loading = init();

  $: console.log(detailData);

  const dispatch = createEventDispatcher();

  export let name: string = "parkpark";

  const testclick = () => {
    dispatch("message", {
      text: name,
    });
  };
</script>

{#await loading}
  <div>로딩중...</div>
{:then}
  <div>name is {detailData[0].name}</div>
{:catch error}
  <div>없는 정보입니다.</div>
{/await}

<!-- <p on:click="{testclick}" style="---border:{border}">
  name is {detailData[0].name}
</p> -->
<style>
  /* p {
    border: var(---border);
    color: blue;
  } */
</style>
