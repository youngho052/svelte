<script lang="ts">
  import { onMount } from "svelte";
  import { useNavigate } from "svelte-navigator";
  import axios from "axios";
  import { API } from "../api/api";
  import App from "../App.svelte";
  import List from "../pages/List.svelte";
  import Modal from "../components/list/Modal.svelte";

  const navigate = useNavigate();

  let listData: any[] = [];
  let visible: boolean = false;

  $: console.log(visible, "<<<<<");
  const init = async () => {
    const response = await axios.get(`${API}/example`);

    listData = await response.data.data.Items;
  };

  onMount(() => {
    init();
  });

  let loading = init();

  $: console.log(listData);
</script>

<div on:click="{() => (visible = true)}">LIST PAGE</div>
{#await loading}
  <p>로딩중 ....</p>
{:then}
  <div class="listBox">
    <Modal visible="{visible}" />
    {#each listData as list}
      <div class="listItem">
        <div class="stackBox">
          <span>기술스택</span>
          {#each list.tech_stack as item}
            <div
              class="stackContainer"
              on:click="{() =>
                navigate(`${list.test_id}`, { state: list.test_id })}"
            >
              <div>
                <span>스택 : </span>
                <span>{item.category} end</span>
              </div>
              <div>
                <span>언어 : </span>
                <span>{item.tech_name}</span>
              </div>
            </div>
          {/each}
        </div>
        <div class="infoBox">
          <span>이름 :</span>
          <span>{list.name}</span>
        </div>
      </div>
    {/each}
  </div>
{/await}

<style>
  .listBox {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px 0;
    border: 1px solid red;
  }

  .listItem {
    display: flex;
    justify-content: space-between;
    width: 50%;
    padding: 20px;
    border: 1px solid blue;
  }

  .stackBox {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .stackContainer {
    display: flex;
    flex-direction: column;
    gap: 10px 0;
    margin-top: 10px;
    padding: 20px;
    border: 1px solid #eee;
  }
</style>
