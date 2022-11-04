<script setup>
import { ref, onMounted, watch } from "vue";

const todos = ref([]);

const input_content = ref("");

const types = ref([
  { id: 1, name: "frontend" },
  { id: 2, name: "backend" },
]);

onMounted(()=>{
localStorage.getItem("todos") && (todos.value = JSON.parse(localStorage.getItem("todos")));
})

const addTodo = () => {
  todos.value.push({
    content: input_content.value,
    done: false,
  });
  localStorage.setItem("todos", JSON.stringify(todos.value));
};

const deletes = (todoIndex) => {
  console.log(todoIndex);
  todos.value.splice(todoIndex, 1);
  localStorage.setItem("todos", JSON.stringify(todos.value));
};
</script>

<template>
  <section class="create-todo">
    <div class="container">
      <div class="row mt-5">
        <h4>Create Todo</h4>
        <form @submit.prevent="addTodo" action="">
          <input class="form-controls" v-model="input_content" type="text" />
          <span>
            <button type="submit">add</button>
          </span>
          <br />
          <select name="" id="">
            <option value="type.id" v-for="item in types">
              {{ item.name }}
            </option>
          </select>

          <table class="table">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Subject</th>
                <th scope="col">Position</th>
                <th scope="col">Setting</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(todoItem, todoIndex) in todos" :key="todoIndex">
                <th scope="row">{{todoIndex +1 }}</th>
                <td>{{ todoItem.content }}</td>
                <td>Otto</td>
                <td>
                    <button @click="deletes(todoIndex)" class="btn btn-danger">Deleted</button>
                </td>
              </tr>
            </tbody>
          </table>
        </form>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
@import "../assets/sass/todo.scss";
</style>
