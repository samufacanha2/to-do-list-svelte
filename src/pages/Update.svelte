<script>
  import MyForm from "../components/MyForm.svelte";
  export let id;
  export let title;
  export let description;
  console.log(id, title, description);
</script>

<div class="container">
  <MyForm update {id} {title} {description} />
</div>
