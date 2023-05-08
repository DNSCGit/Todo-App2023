<template>
  <div class="flex h-screen bg-yellow-700 justify-center">
    <div class="w-full h-96 bg-white rounded shadow-lg mt-8 mx-48">
      <div><p class="text-2xl font-bold my-4 mx-4">To-Do List</p></div>
      <div class="flex mx-12">
        <form @submit.prevent="addTodo" class="flex items-center mb-4">
          <label class="mx-2">New Task:</label>
          <input
            type="text"
            v-model="Task"
            class="rounded-l px-3 py-2 w-full border-4"
            placeholder=""
          />
          <form @submit.prevent="addTodo" class="flex items-center mb-4"></form>
          <label class="mx-2">Description</label>
          <input
            type="text"
            v-model="Discreption"
            class="rounded-l px-3 py-2 w-full border-4"
            placeholder=""
          />
          <label class="mx-2">LevelID</label>
          <input
            type="text"
            v-model="LevelID"
            class="rounded-l px-3 py-2 w-full border-4"
            placeholder=""
          />
          <label class="mx-2">Date Time</label>
          <input
            type="text"
            v-model="DateTime"
            class="rounded-l px-3 py-2 w-full border-4"
            placeholder=""
          />
          <button
            type="button"
            @click="addTodo()"
            class="bg-blue-500 hover:bg-blue-600 text-white font-bold rounded-r px-3 py-2 mx-2"
          >
            Add
          </button>
        </form>
      </div>
      <div class="flex justify-center mr-4">
        <ul>
          <li class="flex flex-row items-center py-2 border-gray-800">
            <table>
              <tr>
                <th class="mr-8">Task</th>
                <th class="mr-8">Description</th>
                <th class="mr-8">LevelID</th>
                <th class="mr-8">Date-Time</th>
                <th class="mr-8">Action</th>
              </tr>
              <tr v-for="(todo, index) in todos" :key="index">
                <td>{{ todo.task }}</td>
                <td>{{ todo.description }}</td>
                <td>{{ todo.levelID }}</td>
                <td>{{ todo.DateTime }}</td>
                <td>
                  <button @click="remove(todo.id)">
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke-width="1.5"
                      stroke="currentColor"
                      class="w-6 h-6"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5m8.25 3v6.75m0 0l-3-3m3 3l3-3M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z"
                      />
                    </svg>
                  </button>
                </td>
              </tr>
            </table>
            <!-- <span class="mr-4">{{ todo.task }}</span>
            <span class="mr-4">{{ todo.description }}</span>
            <span class="mr-4">{{ todo.levelID }}</span>
            <span class="mr-4">{{ todo.DateTime }}</span> -->
            <!-- <button @click="remove(todos.id)">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5m8.25 3v6.75m0 0l-3-3m3 3l3-3M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z"
                />
              </svg>
            </button> -->
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {
    // msg: string,
  },

  data() {
    return {
      Task: "",
      Discreption: "",
      LevelID: "",
      DateTime: "",
      todos: null,
    };
  },
  mounted() {
    this.getAll();
  },
  methods: {
    addTodo() {
      ///let data ={
      //}
      // console.log("click");
      let data = [];
      if (this.Task != null || this.Task != "") {
        data.push(this.Task);
      }
      if (this.Discreption != null || this.Discreption != "") {
        data.push(this.Discreption);
      }
      if (this.LevelID != null || this.LevelID != "") {
        data.push(this.LevelID);
      }
      if (this.DateTime != null || this.DateTime != "") {
        data.push(this.DateTime);
      }
      // console.log(data);
      axios.post("http://localhost:3000/list/addTask", data).then(
        (res) => {
          this.getAll();
        },
        (err) => {
          console.log(err);
        }
      );
      // task: description: if (this.NewOne !== "") {
      //   this.todos.push(this.NewOne);
      //   this.NewOne = "";
      // }
    },
    getAll() {
      axios.get("http://localhost:3000/list/getAll").then(
        (res) => {
          console.log(res.data);
          this.todos = res.data;
        },
        (err) => {
          console.log(err);
        }
      );
    },

    remove(id) {
      // console.log(id);
      axios.delete("http://localhost:3000/list/" + id).then(
        (res) => {
          this.getAll();
        },
        (err) => {
          console.log(err);
        }
      );
      // this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
</style>
