<template>
  <section>
    <h1>ToDoApp</h1>
    <form @submit.prevent="submitTodo">
      <label>New TODO:</label>
      <input required name="newTodo" v-model="newTodo">
      <button >Add new TODO</button>
   </form>
   <button @click="markAllDone">Mark all done</button>
   <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <h3 @click="toggleDone(todo)" class="todo" :class="{done: todo.done}">{{ todo.content }}</h3>
        <button @click="removeTodo(index)">Remove Todo</button>
      </li>
   </ul>
  </section>
</template>

<script>
import { ref } from 'vue';

export default {
  setup () {
    const newTodo = ref('');
    const todos = ref([]);
    function submitTodo () {
      todos.value.push({
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone (todo) {
      todo.done = !todo.done;
    }

    function removeTodo (index) {
      todos.value.splice(index,1);
    }

    function markAllDone() {
      todos.value.map( todo => {todo.done = true});
    }

    return {
      submitTodo,
      newTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.done {
  text-decoration: line-through;
}

.todo {
  cursor: pointer;
}
</style>