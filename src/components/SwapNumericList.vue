<script setup lang="ts">
import {ref} from "vue";
import Draggable from "./Draggable.vue";

const numericListSwap = ref([
  "Item 1",
  "Item 2",
  "Item 3",
  "Item 4",
  "Item 5",
  "Item 6",
  "Item 7",
  "Item 8",
  "Item 9",
  "Item 10",
]);
const isDragging = ref(false);

const handleDragStart = (event: DragEvent, index: number) => {
  isDragging.value = true
  console.log("drag start", index, event);
};

const handleDragOver = (event: DragEvent, index: number) => {
  console.log("drag over", index, event);
};

const handleDrop = (event: DragEvent, index: number) => {
  console.log("drop", index, event);
};

const handleDragEnd = (event: DragEvent, index: number) => {
  isDragging.value = false
  console.log("drag end", index, event);
};
</script>

<template>
  <Draggable
      v-model="numericListSwap"
      class="flex flex-col gap-4"
      drop-class="drop-target"
      :swap="true"
      @drag-start="handleDragStart"
      @drag-over="handleDragOver"
      @drop="handleDrop"
      @drag-end="handleDragEnd"
  >
    <template v-slot="{ item }">
      <div
          class="list-item rounded-lg shadow-lg transition-all duration-300 ease-in-out hover:scale-105 hover:shadow-xl"
          :class="{
    'bg-gradient-to-r from-blue-400 to-green-600': !isDragging,
    'bg-gradient-to-r from-blue-500 to-green-700 opacity-75': isDragging
  }"
      >
        <div
            class="flex items-center justify-between px-4 py-2 text-white"
            :class="{
      'cursor-grab active:cursor-grabbing': !isDragging,
      'cursor-grabbing': isDragging
    }"
        >
          <span class="text-lg font-semibold">{{ item }}</span>
        </div>
      </div>
    </template>
  </Draggable>
</template>
