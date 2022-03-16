<script>
  export let visible;

  $: console.log(visible, "modalt");
</script>

<div class="modal" style="display:{visible ? 'flex' : 'none'}">
  <div class="modalContainer">
    <div
      on:click="{() => {
        visible = false;
      }}"
    >
      나가기
    </div>
  </div>
</div>

<style>
  .modal {
    /* display: flex; */
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
    background-color: #fff;
  }
</style>
