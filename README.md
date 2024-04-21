# Vue3DragNDrop

// description?

## Features

- Drag and drop elements in the list and reordering.
- Drag and drop to swap the elements.

### NPM

```bash
npm install vue3-drag-n-drop
```

### Importing library

You can import the library in your project using the following:

```javascript
import { Draggable } from "vue3-drag-n-drop";
```

### Usage

Pass in the array to v-model (items in the given example). Handle the UI by making a use of v-slot.

```javascript
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
```

### Props

- modelValue: (to be passed in v-model): (Array) The array of items to be displayed and manipulated through drag and drop.
- reorder: (Boolean, default: true) Enable/disable reordering functionality.
- swap: (Boolean, default: false) Enable/disable swapping functionality.
- class: (String, default: "") Additional CSS class to be applied to the container element.

### Events

- dragStart: Emitted when a drag operation starts. Receives the DragEvent and the index of the dragged item.
- dragOver: Emitted when an item is dragged over another item. Receives the DragEvent and the index of the item being dragged over.
- drop: Emitted when an item is dropped. Receives the DragEvent and the index where the item is dropped.
- dragEnd: Emitted when a drag operation ends. Receives the DragEvent and the index of the dragged item.
