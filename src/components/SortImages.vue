<script setup lang="ts">
import {ref} from "vue";
import Draggable from "./Draggable.vue";

const sortItems = ref([
  // create 10 image items using src from unsplash
  {
    src: "https://source.unsplash.com/random/800x600",
  },
  {
    src: "https://source.unsplash.com/random/800x601",
  },
  {
    src: "https://source.unsplash.com/random/800x602",
  },
  {
    src: "https://source.unsplash.com/random/800x603",
  },
  {
    src: "https://source.unsplash.com/random/800x604",
  },
  {
    src: "https://source.unsplash.com/random/800x605",
  },
  {
    src: "https://source.unsplash.com/random/800x606",
  },
  {
    src: "https://source.unsplash.com/random/800x607",
  },
  {
    src: "https://source.unsplash.com/random/800x608",
  },
  {
    src: "https://source.unsplash.com/random/800x609",
  },
  {
    src: "https://source.unsplash.com/random/800x610",
  },
  {
    src: "https://source.unsplash.com/random/800x611",
  },
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
      v-model="sortItems"
      class="flex justify-center flex-wrap gap-4"
      @drag-start="handleDragStart"
      @drag-over="handleDragOver"
      @drop="handleDrop"
      @drag-end="handleDragEnd"
  >
    <template v-slot="{ item }">
      <img :src="item.src" alt="item"
           class="aspect-square w-44 rounded-lg shadow-md transition-transform duration-300 hover:scale-105"/>
    </template>
  </Draggable>
</template>
