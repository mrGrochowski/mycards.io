<template>
  <div
    class="min-h-screen flex flex-shrink-0 flex-grow-0 justify-center items-center bg-gradient-to-r from-gray-600 to-gray-500"
  >
    <a
      href="#"
      class="bg-blue-500 rounded-lg font-bold text-white text-center px-4 py-3 transition duration-300 ease-in-out hover:bg-blue-600"
    >
      Dodaj pierwszą kartę
    </a>
  </div>
</template>

<script setup>
import { defineProps, reactive } from "vue";

defineProps({
  msg: String,
});

const state = reactive({ count: 0 });
</script>
