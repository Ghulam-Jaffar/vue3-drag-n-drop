<template>
  <h1>Draggable Images</h1>
  <p>Drag and drop images to reorder them.</p>
  <label>
    <input type="radio" value="swap" v-model="selectedOption" />
    Swap
  </label>
  <label>
    <input type="radio" value="reorder" v-model="selectedOption" />
    Reorder
  </label>
  <Draggable
    v-model="items"
    class="container"
    :dragClass="'dragItem'"
    :dropClass="'dropItem'"
    :swap="selectedOption === 'swap'"
    :reorder="selectedOption === 'reorder'"
    @drag-start="handleDragStart"
    @drag-over="handleDragOver"
    @drop="handleDrop"
    :customDropHandler="handleCustomDrop"
  >
    <template v-slot="{ item }">
      <img :src="item.src" alt="item" width="200" height="200" />
    </template>
  </Draggable>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Draggable from './components/Draggable.vue';

interface Item {
  src: string;
  isDragging?: boolean;
  isDropping?: boolean;
}

const items = ref<Item[]>(Array.from({ length: 12 }, (_, i) => ({
  src: `https://source.unsplash.com/random/800x60${i}`,
})));

const selectedOption = ref('swap');

const handleDragStart = (event: DragEvent, index: number) => {
  console.log('drag start', index, event);
};

const handleDragOver = (event: DragEvent, index: number) => {
  console.log('drag over', index, event);
};

const handleDrop = (event: DragEvent, index: number) => {
  console.log('drop', index, event);
};

const handleCustomDrop = (DraggedItem:Item,draggedIndex:number,DroppedItem:Item,droppedIndex:number) => {
  // Custom drop handler logic goes here, for example, making an API call
  console.log('Custom drop handler', DraggedItem,draggedIndex,DroppedItem,droppedIndex);
};
</script>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.dragItem {
  border: 2px solid #e02323;
  border-radius: 5px;
  opacity: 0.7;
}
.dropItem {
  border: 2px solid #2c23e0;
  border-radius: 5px;
  opacity: 0.7;
}
</style>
