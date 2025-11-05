<template>
  <div>{{ fullName }}</div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const firstName = ref("Jaehun");
const lastName = ref("Bae");

const fullName = computed(() => {
  return firstName.value + " " + lastName.value;
});

onMounted(() => {
  setTimeout(() => {
    firstName.value = "BJH";
  }, 2000);
});
</script>
