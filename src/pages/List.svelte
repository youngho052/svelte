<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  import { API } from "../api/api";

  let data;

  onMount(async () => {
    const res = await axios.get(`${API}/example`);

    if (res) {
      console.log(res.data.data.Items, "dsadasdas");
      data = res.data.data.Items;
    }
  });

  console.log(data, "<<<");
</script>

<div>list page</div>

<style></style>
