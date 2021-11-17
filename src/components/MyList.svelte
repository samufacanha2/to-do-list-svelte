<script>
  import { onMount } from "svelte";
  import "../styles/MyList.scss";
  import Pencil from "svelte-material-icons/Pencil.svelte";
  import Delete from "svelte-material-icons/Delete.svelte";

  import { Link } from "svelte-routing";
  export let taskList = [];
  onMount(() => {
    fetch("http://localhost:3330/get")
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        taskList = data;
      });
  });
  export let deleteTask = (id) => {
    fetch(`http://localhost:3330/delete/${id}`, {
      method: "DELETE",
    });
  };
</script>

<div class="dashboard">
  {#if taskList.length > 0}
    {#each taskList as task}
      <div class="task-card">
        <div class="text">
          <h1 class="task-title">{task.title}</h1>
          <p class="task-description">{task.description}</p>
        </div>
        <div class="task-options">
          <Link
            to={`/update/${task._id}/${task.title}/${task.description}`}
            class="update"
          >
            <Pencil />
          </Link>
        </div>
        <div class="task-options">
          <div
            class="delete"
            on:click={() => {
              deleteTask(task._id);
              window.location.reload();
            }}
          >
            <Delete />
          </div>
        </div>
      </div>
    {/each}
  {/if}
  {#if taskList.length === 0}
    <div class="empty-tasks">
      Registre uma atividade utilizando os campos acima
    </div>
  {/if}
</div>
