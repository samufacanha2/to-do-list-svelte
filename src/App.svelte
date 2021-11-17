<script>
  import Home from './pages/Home.svelte'
  import Update from './pages/Update.svelte'
  import { Router, Link, Route } from "svelte-routing";
  export let url = "";
</script>

<main>
  <Router url="{url}">
    <div>
      <Route path="/update/:id/:title/:description" let:params  >
        <Update id={params.id} title={params.title} description={params.description} />
      </Route>
      <Route path="/"><Home /></Route>
    </div>
  </Router>
</main>

