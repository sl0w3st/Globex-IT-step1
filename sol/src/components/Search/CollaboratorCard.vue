<script setup lang="ts">
import PhoneIcon from "@/components/icons/PhoneIcon.vue";
import MailIcon from "@/components/icons/MailIcon.vue";
import type { CollaboratorData } from "@/models/Collaborator";

interface CardProps {
  data: CollaboratorData;
}

defineProps<CardProps>();
</script>

<template>
  <a
    href="#"
    class="flex flex-col h-80 p-6 rounded-2xl bg-white border border-gray-200 gap-6 shadow-lg hover:bg-gray-100"
  >
    <h2 class="mb-2 text-2xl font-bold tracking-tight text-gray-900">
      {{ data.name || "No name provided" }}
    </h2>
    <div class="grid grid-cols-[auto_minmax(0,_1fr)] gap-x-4 gap-y-3">
      <PhoneIcon class="place-self-center" />
      <span class="font-normal text-gray-700">
        {{ data.phone || "No phone provided" }}
      </span>
      <MailIcon class="place-self-center" />
      <span class="font-normal text-gray-700">
        {{ data.email || "No email provided" }}
      </span>
    </div>
  </a>
</template>
