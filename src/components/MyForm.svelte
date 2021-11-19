<script>
  import "../styles/MyForm.scss";
  import axios from "axios";

  export let update = false;
  export let id = "";
  export let title = "";
  export let description = "";
  let submitForm = (e) => {
    const form = e.target;
    const title = form.title.value;
    const description = form.description.value;

    axios
      .post("http://localhost:3330/create", { title, description })
      .then(() => (window.location.href = "/"));
  };
  let updateForm = (e) => {
    const form = e.target;
    const title = form.title.value;
    const description = form.description.value;

    axios
      .put(`http://localhost:3330/update/${id}`, { title, description })
      .then(() => (window.location.href = "/"));
  };
  export let goBack = (event) => {
    event.preventDefault();
    window.location.href = "/";
  };
</script>

<form on:submit|preventDefault={update ? updateForm : submitForm}>
  <label class={title ? "visible" : ""} for="title">Titulo</label>
  <input
    type="text"
    id="title"
    name="title"
    placeholder="Digite um titulo"
    bind:value={title}
  />

  <label class={description ? "visible" : ""} for="description">Descrição</label
  >
  <input
    type="text"
    id="description"
    name="description"
    placeholder="Digite uma descrição"
    bind:value={description}
  />

  {#if !update}
    <button type="submit">Adicionar</button>
  {/if}

  {#if update}
    <div class="footer-buttons">
      <button on:click={goBack}>Voltar</button>
      <button type="submit">Salvar</button>
    </div>
  {/if}
</form>
