<script setup lang="ts">
import { ref } from "vue";
import Draggable from "./components/Draggable.vue";

const items = ref([
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

const handleDragStart = (event: DragEvent, index: number) => {
  console.log("drag start", index, event);
};

const handleDragOver = (event: DragEvent, index: number) => {
  console.log("drag over", index, event);
};

const handleDrop = (event: DragEvent, index: number) => {
  console.log("drop", index, event);
};
</script>

<template>
  <Draggable
    v-model="items"
    class="container"
    @drag-start="handleDragStart"
    @drag-over="handleDragOver"
    @drop="handleDrop"
  >
    <template v-slot="{ item }">
      <img :src="item.src" alt="item" width="200" height="200" />
    </template>
  </Draggable>
</template>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
</style>
