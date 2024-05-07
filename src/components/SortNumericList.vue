<script setup lang="ts">
import {ref} from "vue";
import Draggable from "./Draggable.vue";

const numericListSort = ref([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
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
      v-model="numericListSort"
      class="flex flex-col gap-4"
      drop-class="drop-target"
      @drag-start="handleDragStart"
      @drag-over="handleDragOver"
      @drop="handleDrop"
      @drag-end="handleDragEnd"
  >
    <template v-slot="{ item }">
      <div
          class="list-item rounded-lg shadow-lg transition-all duration-300 ease-in-out hover:scale-105 hover:shadow-xl"
          :class="{
    'bg-gradient-to-r from-purple-400 to-pink-600': !isDragging,
    'bg-gradient-to-r from-purple-500 to-pink-700 opacity-75': isDragging
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
