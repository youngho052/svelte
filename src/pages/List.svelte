<script lang="ts">
  import { onMount, afterUpdate, beforeUpdate } from 'svelte';
  import { useNavigate } from 'svelte-navigator';
  import axios from 'axios';
  import { API } from '../api/api';
  import Modal from '../components/list/Modal.svelte';
  import Box from '../components/list/Box.svelte';
  import Row from '../components/common/Row.svelte';
  import Text from '../components/common/Text.svelte';

  const navigate = useNavigate();

  let listData: any[] = [];
  let visible: boolean = false;
  let info: {
    test_id: string;
    name: string;
    category: string;
    tech_name: string;
    level: number;
  } = { test_id: '', name: '', category: '', tech_name: '', level: 1 };

  $: console.log(visible, '<<<<<');
  const init = async () => {
    const response = await axios.get(`${API}/example`);

    listData = await response.data.data.Items;
  };

  // onMount(() => {
  //   init();
  // });

  // beforeUpdate(() => {
  //   init();
  // });

  // afterUpdate(() => {
  //   init();
  // });

  let loading = init();

  const modalClick = () => {
    visible = !visible;
  };

  const addHandle = async () => {
    const res = await axios.post(`${API}/example`, {
      test_id: info.test_id,
      name: info.name,
      tech_stack: [
        {
          category: info.category,
          tech_name: info.tech_name,
          level: Number(info.level),
        },
      ],
    });

    if (res.data.message === 'success') {
      visible = false;
      init();
    }
  };

  const deleteHandle = async (id: string) => {
    const res = await axios.delete(`${API}/example/${id}`, {
      data: {
        test_id: id,
      },
    });
  };

  $: console.log(listData);
  $: console.log(info, 'parent');
</script>

<Text size="20px" on:click="{() => console.log('click')}">LIST PAGE</Text>
<div class="addContainer">
  <div style="width:50%;text-align:right">
    <span style="cursor: pointer;" on:click="{modalClick}">추가</span>
  </div>
</div>

{#await loading}
  <p>로딩중 ....</p>
{:then}
  <div class="listBox">
    {#if visible}
      <Modal bind:info modalClick="{modalClick}" addHandle="{addHandle}" />
    {/if}
    {#each listData as list}
      <Box on:click="{() => navigate(`${list.test_id}`, { state: list.test_id })}">
        <div class="stackBox">
          <Text>기술 스택</Text>
          <!-- <Row gap="0 30px"> -->
          {#each list.tech_stack as item}
            <div class="stackContainer">
              <Row gap="0 5px" justify="flex-start">
                <Text size="16px" color="blue">스택 :</Text>
                <Text size="16px">{item.category}</Text>
              </Row>
              <Row gap="0 5px" justify="flex-start">
                <Text size="16px">언어 :</Text>
                <Text size="16px">{item.tech_name}</Text>
              </Row>
              <Row gap="0 5px" justify="flex-start">
                <Text size="16px">레벨 :</Text>
                <Text size="16px">{item.level}</Text>
              </Row>
            </div>
          {/each}
          <!-- </Row> -->
        </div>
        <div class="infoBox">
          <div>
            <span
              style="cursor: pointer;"
              on:click="{() => {
                deleteHandle(list.test_id);
              }}"
            >
              삭제
            </span>
          </div>
          <div>
            <span>이름 :</span>
            <span>{list.name}</span>
          </div>
        </div>
      </Box>
    {/each}
  </div>
{/await}

<style>
  .addContainer {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 20px 0;
  }

  .listBox {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px 0;
  }

  .stackBox {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .stackContainer {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 10px 0;
    margin-top: 10px;
    padding: 20px;
    border: 1px solid #eee;
  }

  .infoBox {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-end;
  }
</style>
