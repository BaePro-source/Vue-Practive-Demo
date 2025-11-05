<template>
  <div>
    <input ref="inputField" type="text" placeholder="Click the button to focus" />
    <button @click="focusInput">Focus Input</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const inputField = ref(null);

const focusInput = () => {
  inputField.value.focus();
};

onMounted(() => {
  console.log(inputField);
  if(inputField.value) {
    inputField.value.focus();
  }
});
</script>
