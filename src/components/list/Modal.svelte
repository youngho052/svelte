<script lang="ts">
  import InputForm from "./InputForm.svelte";

  export let info: {
    test_id: string;
    name: string;
    category: string;
    tech_name: string;
    level: number;
  };

  export let modalClick: () => void;
  export let addHandle: () => void;

  $: console.log(info, "child");
</script>

<div class="modal">
  <div class="modalContainer">
    <div style="text-align: right;cursor:pointer" on:click="{modalClick}">
      나가기
    </div>
    <div class="infoContainer">
      <!-- {#each Object.keys(info) as item}
        <InputForm>
          <span slot="info">{item}</span>
          <input bind:value="{info[item]}" slot="input" />
        </InputForm>
      {/each} -->
      <InputForm>
        <span slot="info">ID</span>
        <input bind:value="{info.test_id}" slot="input" />
      </InputForm>
      <InputForm>
        <span slot="info">Name</span>
        <input bind:value="{info.name}" slot="input" />
      </InputForm>
      <InputForm>
        <span slot="info">Category</span>
        <input bind:value="{info.category}" slot="input" />
      </InputForm>
      <InputForm>
        <span slot="info">Tech</span>
        <input bind:value="{info.tech_name}" slot="input" />
      </InputForm>
      <InputForm>
        <span slot="info">Level</span>
        <input bind:value="{info.level}" slot="input" />
      </InputForm>
    </div>
    <div
      style="text-align: right;cursor:pointer;margin-top:10px"
      on:click="{addHandle}"
    >
      저장
    </div>
  </div>
</div>

<style>
  .modal {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;

    width: 100%;
    height: 100vh;
    bottom: 0;
    background-color: rgb(0, 0, 0, 0.3);
  }

  .modalContainer {
    width: 400px;
    height: 700px;
    padding: 30px 20px;
    background-color: #fff;
  }

  .infoContainer {
    display: flex;
    flex-direction: column;
    gap: 10px 0;
    margin-top: 15px;
  }

  input {
    width: 70%;
  }
</style>
