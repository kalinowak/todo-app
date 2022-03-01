<template>
  <div class="home">
    <h1>ToDo App</h1>
    <form @submit.prevent="addTodo()">
      <label>New ToDo</label>
      <input
        v-model="newTodo"
        type="text"
        name="newTodo"
        autocomplete="off" />

      <button>Add ToDo</button>

    </form>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {
  },
};
</script>
