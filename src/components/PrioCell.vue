<template>
  <div class="prio-cell">
    <input
      v-show="isInputShown"
      v-model="newTask"
      ref="taskInput"
      @keyup.enter="onInput(newTask)"
      placeholder="Add task"
    />
    <ul>
      <li v-for="item in items">
        <span @click="onSelection(item)">{{ item }}</span>
        <button @click="deleteItem(item)">remove</button>
      </li>
    </ul>
    <div class="right-alignment">
      <button @click="showInput">+</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { Ref, ref } from "vue";

const items: Ref<string[]> = ref([]);
const taskInput = ref(null);
const isInputShown = ref(false);
const newTask = ref("");

function showInput() {
  isInputShown.value = true;
  taskInput.value.focus();
}

function deleteItem(item: string) {
  console.log(`deleting item ${item}`);
  const i = items.value.indexOf(item);
  items.value.splice(i, 1);
}

function onSelection(item: string) {
  console.log(`selected item ${item}`);
}

function onInput(input: string) {
  items.value.push(input);
  isInputShown.value = false;
  newTask.value = "";
}
</script>

<style>
.right-alignment {
  text-align: right;
}
button {
  margin-left: 1rem;
}
ul {
  list-style-type: none;
}
.prio-cell {
  height: 100%;
}
</style>
