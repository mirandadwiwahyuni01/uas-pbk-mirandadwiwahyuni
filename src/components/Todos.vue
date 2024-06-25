<script setup>
import { ref, computed } from "vue";

const newTodo = ref("");
const hideCompleted = ref(false);
let id = 0;
const todos = ref([]);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>
  <div class="wrapper">
    <header>
      <h1>List Bunga</h1>
    </header>
    <main>
      <section class="sec a1">
        <p class="judul">Tambah Bunga</p>
        <div class="wrapperleft">
          <div class="tambah">
            <form @submit.prevent="addTodo">
              <input
                id="main-input"
                v-model="newTodo"
                required
                placeholder="Add Todo List..."
              />
              <button>Tambah</button>
            </form>
          </div>
          <div class="info">
            <p>
              Ada <span>{{ todos.length }}</span> Bunga di list
            </p>
            <p>
              <span>{{ todos.filter((todo) => todo.done).length }}</span> Selesai
            </p>
            <p>
              <span>{{ todos.filter((todo) => !todo.done).length }}</span> Belum
            </p>
          </div>
          <div class="filter">
            <button @click="hideCompleted = !hideCompleted">
              {{ hideCompleted ? "Lihat Selesai" : "Sembunyikan Selesai" }}
            </button>
          </div>
        </div>
      </section>
      <section class="sec a2">
        <p class="judul">Ini List Bungamu</p>
        <ul>
          <li
            v-for="todo in filteredTodos"
            :key="todo.id"
            :class="{ done: todo.done }"
          >
            <input type="checkbox" v-model="todo.done" />
            <span :class="{ done: todo.done }">{{ todo.text }}</span>
            <button @click="removeTodo(todo)">Hapus</button>
          </li>
        </ul>
      </section>
    </main>
  </div>
</template>

<style scoped>
body {
  background: #cdc19d;
  font-family: "Mulish", sans-serif;
  color: #ae6c6c;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.wrapper {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 80%;
  max-width: 1200px;
  background: #ffffff;
  border-radius: 15px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

header {
  margin-bottom: 20px;
}

h1 {
  color: #9a408b;
  font-family: "Jersey 25", sans-serif;
  font-weight: 500;
  font-size: 3rem;
}

main {
  display: flex;
  width: 100%;
  justify-content: space-between;
}

section {
  background-color: #f0f0f0;
  width: 45%;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.judul {
  margin-bottom: 10px;
  font-size: 1.5rem;
  background-color: #e9bfbf;
  padding: 10px;
  border-radius: 15px;
  color: #333;
  text-align: center;
}

.wrapperleft {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 80%;
}

.tambah form {
  display: flex;
  justify-content: space-between;
}

#main-input {
  border: none;
  padding: 10px;
  border-radius: 10px;
  background: #e0e0e0;
  transition: 0.3s;
  width: 70%;
}

#main-input:focus {
  outline: none;
  background: #ffffff;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

button {
  background-color: #5dd59d;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  color: #fff;
  font-family: "JetBrains Mono", monospace;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45c287;
}

button:focus {
  outline: none;
}

.info {
  font-size: 1rem;
  text-align: center;
}

.info span {
  color: cadetblue;
}

.filter {
  display: flex;
  justify-content: center;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  max-height: 300px;
  overflow-y: auto;
}

ul li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #fff;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

ul li.done {
  background-color: #41b06e;
}

ul li span.done {
  text-decoration: line-through;
  color: #fff;
}

ul li input {
  margin-right: 10px;
  transform: scale(1.5);
}

ul li button {
  background-color: #e57373;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s;
}

ul li button:hover {
  background-color: #4b9299;
}
</style>
