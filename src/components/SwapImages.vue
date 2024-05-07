<script setup lang="ts">
import {ref} from "vue";
import Draggable from "./Draggable.vue";

const swapItems = ref([
  // create 10 image items using src from unsplash
  {
    src: "https://source.unsplash.com/random/800x623",
  },
  {
    src: "https://source.unsplash.com/random/800x622",
  },
  {
    src: "https://source.unsplash.com/random/800x621",
  },
  {
    src: "https://source.unsplash.com/random/800x620",
  },
  {
    src: "https://source.unsplash.com/random/800x619",
  },
  {
    src: "https://source.unsplash.com/random/800x618",
  },
  {
    src: "https://source.unsplash.com/random/800x617",
  },
  {
    src: "https://source.unsplash.com/random/800x616",
  },
  {
    src: "https://source.unsplash.com/random/800x615",
  },
  {
    src: "https://source.unsplash.com/random/800x614",
  },
  {
    src: "https://source.unsplash.com/random/800x613",
  },
  {
    src: "https://source.unsplash.com/random/800x612",
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
      v-model="swapItems"
      class="flex justify-center flex-wrap gap-4"
      :swap="true"
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
