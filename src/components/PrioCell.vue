<template>
  <div class="prio-cell">
    <input
      v-show="isInputShown"
      v-model="newTask"
      ref="taskInput"
      @keyup.enter="onInput(newTask)"
      @blur="onInput(newTask)"
      placeholder="Add task"
    />
    <ul>
      <li v-for="item in items" class="container">
        <span @click="onSelection(item)">{{ item }}</span>
        <div>
          <button @click="completeItem(item)">
            <img src="../assets/tick.gif" :height="imgSize" :width="imgSize" />
          </button>
          <button @click="deleteItem(item)">
            <img src="../assets/trash.gif" :height="imgSize" :width="imgSize" />
          </button>
        </div>
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
const imgSize = 20;

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
  if (input.trim() !== "") {
    items.value.push(input);
    addSound.play();
  }
  isInputShown.value = false;
  newTask.value = "";
}
</script>

<style>
.right-alignment {
  text-align: right;
}
button {
  padding: 0.3em 1em;
}
ul {
  list-style-type: none;
  padding-inline-start: 0px;
}
.prio-cell {
  height: 100%;
}
.container {
  display: flex;
  justify-content: space-between;
  gap: 5em;
}
</style>
