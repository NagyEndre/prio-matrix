<script lang="ts" setup>
import PrioCell from "./PrioCell.vue";

const prios = ["HIGH", "MID", "LOW"];

function getClass(prio: string) {
  return prio.toLowerCase();
}
</script>

<template>
  <table>
    <tr>
      <th class="space-cell"></th>
      <th class="space-cell"></th>
      <th colspan="3" class="title">Urgency</th>
    </tr>
    <tr>
      <th class="space-cell"></th>
      <th class="space-cell"></th>
      <th v-for="prio in prios" :class="getClass(prio)" class="col-width">
        {{ prio }}
      </th>
    </tr>

    <tr>
      <th rowspan="4" class="title">Impact</th>
    </tr>
    <tr v-for="prio in prios">
      <th :class="getClass(prio)">{{ prio }}</th>
      <td v-for="index in 3">
        <prio-cell></prio-cell>
      </td>
    </tr>
  </table>
</template>

<style>
th,
td {
  border: 1px solid grey;
  border-radius: 0.2rem;
  padding: 0.5rem;
}
.title {
  background-color: cornflowerblue;
}
.high {
  background: red;
}
.mid {
  background: yellow;
}
.low {
  background: green;
}
.col-width {
  min-width: 10rem;
}
.space-cell {
  border: none;
}
</style>
