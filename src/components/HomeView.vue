<script setup lang="ts">
import { ref } from "vue";
let id = ref<number>(0);
let newTodo = ref("");
const datas = ref<
  {
    id: number;
    text: string;
    done: boolean;
  }[]
>([
  { id: id.value++, text: "breakfast", done: false },
  { id: id.value++, text: "bath", done: false },
  { id: id.value++, text: "study", done: false },
]);
function addTodo() {
  datas.value.push({ id: id.value++, text: newTodo.value, done: false });
  newTodo.value = "";
}
function removeTodo(todo: object) {
  datas.value = datas.value.filter((i) => {
    return i != todo;
  });
}
</script>

<template>
  <div class="text-center">
    <h1 class="text-[30px] text-center font-bold text-red-800">Vue Todo App</h1>
    <br />
    <input
      class="
        text-center
        w-1/5
        placeholder:italic placeholder:text-slate-400
        bg-white
        border border-slate-300
        rounded-md
        py-2
        pl-9
        pr-3
        shadow-sm
        focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1
        sm:text-sm
      "
      placeholder="add item "
      type="text"
      v-model="newTodo"
    />
    <button
      class="
        bg-transparent bg-slate-400
        hover:bg-slate-500
        ml-6
        text-black
        font-bold
        py-1
        px-4
        border
        hover:border-x-stone-400-500
        rounded
      "
      v-on:click="addTodo"
    >
      Add Todo
    </button>

    <ul class="list-disc text-black">
      <div class="flex flex-col justify-start items-start w-72 m-auto">
        <li
          v-for="todo in datas"
          :key="todo.id"
          class="text-[25px] capitalize leading-6 m-4 text-yellow-50"
        >
          <input
            type="checkbox"
            class="h-6 w-8 align-middle"
            name=""
            id=""
            v-model="todo.done"
          />
          <span
            class="bg-slate-600 p-2 rounded-lg"
            :class="{ done: todo.done }"
            >{{ todo.text }}</span
          >
          <button
            @click="removeTodo(todo)"
            class="text-red-500 text-[20px} px-2 ml-2"
          >
            X
          </button>
        </li>
      </div>
    </ul>
  </div>
</template>
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
