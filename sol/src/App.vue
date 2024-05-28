<template>
  <div
    id="collaboratorInfoModal"
    class="hidden absolute top-0 left-0 right-0 bottom-0 w-screen h-screen z-50"
  >
    <div class="relative h-full w-full bg-gray-500 opacity-20" />
    <div
      class="absolute inset-0 my-auto w-5/6 md:w-1/2 xl:w-1/3 mx-auto flex flex-col h-min p-6 rounded-2xl bg-white border border-gray-200 gap-6 shadow-lg"
    >
      <div class="flex justify-between items-center">
        <h2
          class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
        >
          {{ selectedCollaborator?.name || "No name provided" }}
        </h2>
        <button
          id="collaboratorInfoModalCloseButton"
          v-on:click="closeCollaboratorModal()"
        >
          <XIcon />
        </button>
      </div>
      <div
        class="grid md:grid-cols-[auto_minmax(0,_1fr)] grid-cols-1 gap-x-4 gap-y-3"
      >
        <span class="text-black text-lg"> Телефон: </span>
        <span class="text-gray-400">
          {{ selectedCollaborator?.phone || "No phone provided" }}
        </span>

        <span class="text-black text-lg"> Почта: </span>
        <span class="text-gray-400">
          {{ selectedCollaborator?.email || "No email provided" }}
        </span>

        <span class="text-black text-lg"> Дата приема: </span>
        <span class="text-gray-400">
          {{ selectedCollaborator?.hire_date || "No hire_date provided" }}
        </span>

        <span class="text-black text-lg"> Должность: </span>
        <span class="text-gray-400">
          {{
            selectedCollaborator?.position_name || "No position_name provided"
          }}
        </span>

        <span class="text-black text-lg"> Подразделение: </span>
        <span class="text-gray-400">
          {{ selectedCollaborator?.department || "No department provided" }}
        </span>
      </div>
      <p class="text-gray-400 col-span-2">
        <span class="block text-black text-lg col-span-2">
          Дополнительная информация:
        </span>
        Разработчики используют текст в качестве заполнителя макта страницы.
      </p>
    </div>
  </div>

  <div
    class="items-center justify-center h-screen bg-gray-50 px-2 md:px-20 py-16"
  >
    <SearchBar class="mb-8" v-model="searchTerm" />
    <div class="grid lg:grid-cols-3 md:grid-cols-2 grid-cols-1 gap-8">
      <CollaboratorCard
        v-for="(item, index) in collaboratorList"
        :data="item"
        :key="index"
        v-on:click="() => showCollaboratorModal(item)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, watch } from "vue";
import CollaboratorCard from "@/components/Search/CollaboratorCard.vue";
import SearchBar from "@/components/Search/SearchBar.vue";
import XIcon from "@/components/icons/XIcon.vue";
import { CollaboratorData } from "./models/Collaborator";

const collaboratorList = ref<CollaboratorData[]>([]);
const searchTerm = ref("");
const selectedCollaborator = ref<CollaboratorData | null>(null);

const showCollaboratorModal = (data: CollaboratorData): void => {
  selectedCollaborator.value = data;
  const modalElement = document.querySelector("#collaboratorInfoModal");
  if (modalElement) modalElement.classList.remove("hidden");
};

const closeCollaboratorModal = () => {
  const modalElement = document.querySelector("#collaboratorInfoModal");
  if (modalElement) modalElement.classList.add("hidden");
};

watch(searchTerm, async (newTerm) => {
  await search(newTerm);
});

const search = async (term?: String) => {
  const full_uri = "http://localhost:3000" + (term ? "?term=" + term : "");
  const response = await fetch(full_uri);
  const data = await response.json();
  console.log("successful fetch", { data });
  collaboratorList.value = data;
};

onMounted(async () => {
  await search();
});
</script>
