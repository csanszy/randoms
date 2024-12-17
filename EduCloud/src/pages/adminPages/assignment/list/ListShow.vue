<template>
  <div v-if="selectedItem" class="mt-6">
    <h2 class="text-xl font-bold">Modul tartalma</h2>

    <!-- Table displaying the selected item's properties -->
    <div class="border rounded-md bg-gray-400">

      <table class="min-w-[30dvw] text-center">
        <thead>
        <tr>
          <th class="px-4 border">Név</th>
          <th class="px-4 border">File</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item, index) in selectedItem.items" :key="index" class="odd:bg-gray-200 even:bg-gray-300">
          <td>
            {{ item.name }}
          </td>
          <td>
            <button><!-- Handle File opening -->
            {{ item.fileName }}
            </button>
          </td>
        </tr>
        </tbody>
      </table>

    </div>
    <div class="flex justify-center">
      <p class="text-gray-500">A megnyitáshoz kattintsno a fálj nevére.</p>
    </div>
  </div>
  <div v-else>
    <p class="text-gray-500">Kattintson az egyik modulra a továbbiakhoz.</p>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

// Define the prop the child will receive
const props = defineProps({
  selectedItem: Object,
});
</script>