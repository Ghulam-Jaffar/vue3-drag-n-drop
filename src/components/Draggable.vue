<script setup lang="ts">
import { defineEmits, defineProps } from "vue";

const emit = defineEmits([
  "dragStart",
  "dragOver",
  "drop",
  "dragEnd",
  "input",
  "update:modelValue",
]);

const props = defineProps({
  modelValue: {
    type: Array,
    required: true,
  },
  reorder: {
    type: Boolean,
    default: true,
  },
  swap: {
    type: Boolean,
    default: false,
  },
  class: {
    type: String,
    default: "",
  },
});

// not necessary since emitting in handleDrop method
// watch(
//   () => props.modelValue,
//   (newValue) => {
//     emit("update:modelValue", newValue); // sync with v-model
//   }
// );

const handleDragStart = (event: DragEvent, index: number) => {
  event.dataTransfer!.setData("text/plain", index.toString());
  emit("dragStart", event, index);
};

const handleDragOver = (event: DragEvent, index: number) => {
  event.preventDefault();
  emit("dragOver", event, index);
};

const handleDrop = (event: DragEvent, index: number) => {
  const draggedIndex = Number(event.dataTransfer!.getData("text/plain"));
  const draggedItem = props.modelValue[draggedIndex];
  emit("drop", event, index);

  if (props.swap) {
    const newItems = [...props.modelValue];
    newItems[draggedIndex] = props.modelValue[index];
    newItems[index] = draggedItem;
    emit("update:modelValue", newItems);
  } else if (props.reorder) {
    // Only perform reordering if swap is false
    const newItems = [...props.modelValue];
    newItems.splice(draggedIndex, 1);
    newItems.splice(index, 0, draggedItem);
    emit("update:modelValue", newItems);
  }
};
</script>

<template>
  <div :class="class">
    <template v-for="(item, index) in modelValue" :key="index">
      <div
        draggable="true"
        @dragstart="handleDragStart($event, index)"
        @dragover="handleDragOver($event, index)"
        @drop="handleDrop($event, index)"
        @dragend="$emit('dragEnd', $event, index)"
      >
        <slot :item="item"></slot>
      </div>
    </template>
  </div>
</template>
