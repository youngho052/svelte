<script lang="ts">
  import router from "page";
  import routes from "./routes";
  import { Router, Route, useNavigate, Link } from "svelte-navigator";
  import { API } from "./api/api";

  import List from "./routes/List.svelte";
  import Detail from "./routes/Detail.svelte";

  import axios from "axios";
  import { createEventDispatcher } from "svelte";
  import { writable } from "svelte/store";
  // import List from "./pages/List.svelte";

  let page: typeof List;
  let params: string;

  routes.forEach((item) => {
    router(
      item.path,
      (ctx, next) => {
        params = ctx.params;
        next();
      },

      () => {
        page = item.component;
      }
    );
  });

  router.start();

  let user: { login: boolean } = { login: false };

  const { subscribe } = writable(0);
  //  let items:any[];

  // const init = async() => {
  // 	const res = await axios.get(`${API}/example`);
  // 	items = res.data.data.Items;

  // }

  // init();
  const count = writable(0);

  const clickmessage = (event: { detail: { text: string } }) => {
    alert(event.detail.text);
  };

  export let name: string;
  let test: { id: number; name: string }[] = [
    {
      id: 1,
      name: "hi",
    },
    {
      id: 2,
      name: "hello",
    },
  ];
</script>

<Router url="">
  <header>
    <nav>
      <Link to="list">List</Link>
    </nav>
  </header>
  <main>
    <Route path="list" component="{List}" />
    <Route path="list/:id" component="{Detail}" />
  </main>
</Router>

<!-- <Router>
  <main>
    <Route path="/">
      <h1>Hello {name}!</h1>
      <p>
        Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
        how to build Svelte apps.
      </p>
    </Route>
    <svelte:component this="{List}" params="/list" />
    <Route path="test">
      <Test name="park" on:message="{clickmessage}" border="1px solid red" />
      <Test />
    </Route>
    <Route path="list" component="{List}" />

    {#each test as item}
      <p>{item.name}</p>
    {/each}
  </main>
</Router> -->
<style>
  header {
    display: flex;
    align-items: center;
    justify-content: center;

    padding: 20px;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  }

  nav {
    display: flex;
    gap: 0 30px;
  }

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
