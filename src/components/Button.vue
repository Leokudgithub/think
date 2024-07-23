<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  sym: [Number, String],
  foo: Function, // Указываем тип foo как функцию
});
</script>

<template>
  <button @click="foo"> {{ sym }} </button> <!-- Вызываем foo без скобок -->
</template>

<style scoped>
/* Стили для кнопки */
</style>