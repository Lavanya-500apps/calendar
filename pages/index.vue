<template>
    <div>
      <collectionMain :weekDays="day" />
    </div>
  </template>
  <script setup lang="ts">
  import { ref } from "vue";
  const day = ref(["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]);
  </script>