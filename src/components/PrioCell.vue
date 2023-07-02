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
        <button @click="completeItem(item)">done</button>
        <button @click="deleteItem(item)">
          <img src="../assets/trash.gif" height="32" width="32" />
        </button>
      </li>
    </ul>
    <div class="right-alignment">
      <button @click="showInput">+</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { Ref, ref } from "vue";
import DiscordConnect from "../assets/discord-connect.mp3";
import Pew from "../assets/pew.mp3";
import LegoBreak from "../assets/lego-breaking.mp3";

const items: Ref<string[]> = ref([]);
const taskInput = ref(null);
const isInputShown = ref(false);
const newTask = ref("");

const deleteSound = new Audio(LegoBreak);
const addSound = new Audio(DiscordConnect);
const completeSound = new Audio(Pew);

function showInput() {
  isInputShown.value = true;
  taskInput.value.focus();
}

function deleteItem(item: string) {
  console.log(`deleting item ${item}`);
  const i = items.value.indexOf(item);
  deleteSound.play();
  items.value.splice(i, 1);
}

function completeItem(item: string) {
  console.log(`completing item ${item}`);
  const i = items.value.indexOf(item);
  completeSound.play();
  items.value.splice(i, 1);
}

function onSelection(item: string) {
  console.log(`selected item ${item}`);
}

function onInput(input: string) {
  items.value.push(input);
  addSound.play();
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
  padding: 0.3em 1em;
}
ul {
  list-style-type: none;
}
.prio-cell {
  height: 100%;
}
</style>
