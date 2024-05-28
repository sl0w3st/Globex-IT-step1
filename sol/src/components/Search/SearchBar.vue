<script setup lang="ts">
import SearchIcon from "../icons/SearchIcon.vue";

const searchTerm = defineModel();
</script>

<template>
  <div class="w-full">
    <label
      for="default-search"
      class="mb-2 text-sm font-medium text-gray-900 sr-only"
      >Search</label
    >
    <div class="relative">
      <input
        type="search"
        id="employee-search"
        class="block w-full p-4 ps-10 text-sm text-gray-900 border border-gray-300 rounded-full bg-gray-50 focus:ring-blue-500 focus:border-blue-500"
        required
        v-model="searchTerm"
      />
      <SearchIcon
        class="absolute inset-y-0 right-0 my-auto mx-5 pointer-events-none"
      />
    </div>
  </div>
</template>
