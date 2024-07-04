```markdown
# Vue3DragNDrop

Vue3DragNDrop is a Vue 3 library that enables drag-and-drop functionality within lists, allowing for both reordering and swapping of elements.

## Features

- Drag and drop elements in the list for reordering.
- Drag and drop to swap elements.
- Customizable drag and drop classes and event handling.

## Installation

Install the library using npm:

```bash
npm install vue3-drag-n-drop
```

## Importing the Library

You can import the library in your project using the following:

```javascript
import { Draggable } from "vue3-drag-n-drop";
```

## Usage

Pass in the array to `v-model` (items in the given example). Handle the UI by making use of `v-slot`.

```vue
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

<script setup lang="ts">
import { ref } from "vue";

const items = ref([
  { src: "https://example.com/image1.jpg" },
  { src: "https://example.com/image2.jpg" },
  // Add more items as needed
]);

const handleDragStart = (event, index) => {
  console.log("Drag started:", index);
};

const handleDragOver = (event, index) => {
  event.preventDefault(); // Necessary to allow dropping
  console.log("Drag over:", index);
};

const handleDrop = (event, index) => {
  console.log("Dropped at index:", index);
};
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
</style>
```

## Props

- `modelValue` (Array, required): The array of items to be displayed and manipulated through drag and drop.
- `reorder` (Boolean, default: true): Enable/disable reordering functionality.
- `swap` (Boolean, default: false): Enable/disable swapping functionality.
- `class` (String, default: ""): Additional CSS class to be applied to the container element.
- `dragClass` (String, default: "dragging"): CSS class applied to the item being dragged.
- `dropClass` (String, default: "drop-target"): CSS class applied to the item being dragged over.
- `customDropHandler` (Function, default: null): Custom handler function for drop events.

## Events

- `dragStart`: Emitted when a drag operation starts. Receives the `DragEvent` and the index of the dragged item.
- `dragOver`: Emitted when an item is dragged over another item. Receives the `DragEvent` and the index of the item being dragged over.
- `drop`: Emitted when an item is dropped. Receives the `DragEvent` and the index where the item is dropped.
- `dragEnd`: Emitted when a drag operation ends. Receives the `DragEvent` and the index of the dragged item.

## Example

Here’s a full example integrating the `Draggable` component in a Vue 3 application:

```vue
<template>
  <div>
    <h1 class="text-6xl text-center mt-10">Vue3DragNDrop Example</h1>
    <Draggable
      v-model="items"
      class="container"
      drag-class="dragging"
      drop-class="drop-target"
      @drag-start="handleDragStart"
      @drag-over="handleDragOver"
      @drop="handleDrop"
      @drag-end="handleDragEnd"
    >
      <template v-slot="{ item }">
        <div class="item">
          <img :src="item.src" alt="item" width="200" height="200" />
        </div>
      </template>
    </Draggable>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Draggable } from "vue3-drag-n-drop";

const items = ref([
  { src: "https://random-image-pepebigotes.vercel.app/api/random-image" },
  { src: "https://random-image-pepebigotes.vercel.app/api/random-image" },
  { src: "https://random-image-pepebigotes.vercel.app/api/random-image" },
  { src: "https://random-image-pepebigotes.vercel.app/api/random-image" },
  { src: "https://random-image-pepebigotes.vercel.app/api/random-image" },
]);

const handleDragStart = (event, index) => {
  console.log("Drag started:", index);
};

const handleDragOver = (event, index) => {
  event.preventDefault(); // Necessary to allow dropping
  console.log("Drag over:", index);
};

const handleDrop = (event, index) => {
  console.log("Dropped at index:", index);
};

const handleDragEnd = (event, index) => {
  console.log("Drag ended:", index);
};
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.item {
  width: 200px;
  height: 200px;
  overflow: hidden;
}

.dragging {
  opacity: 0.5;
  transform: scale(1.1);
  transition: opacity 0.2s, transform 0.2s;
}

.drop-target {
  border: 2px dashed #4299e1;
  transition: border-color 0.2s;
}

.dropped {
  animation: dropped 0.5s;
}

@keyframes dropped {
  0% {
    transform: translateY(-20px);
    opacity: 0;
  }

  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
</style>
```
