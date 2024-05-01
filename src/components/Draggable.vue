<script setup lang="ts">
import { ref } from 'vue';

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
  dragClass: {
    type: String,
    default: "",
  },
  dropClass: {
    type: String,
    default: "",
  },
  customDropHandler: {
    type: Function,
    default: null,
  },
});

const startItem = ref<Element | null>(null);
const startIndex = ref<number | null>(null);
const prevItem = ref<Element | null>(null);

const handleDragStart = (event: DragEvent, index: number) => {
  event.dataTransfer!.setData("text/plain", index.toString());
  let target = event.target as HTMLElement;
  target.classList.add(props.dragClass)
  startItem.value = target;
  startIndex.value = index;
  emit("dragStart", event, index);
};

const handleDragOver = (event: DragEvent, index: number) => {
  event.preventDefault();
  
  let target = event.target as HTMLElement; 
  if(startItem.value === target){
    prevItem.value?.classList.remove(props.dropClass)
    return;
  }

  if (target !== prevItem.value) {
    target.classList.add(props.dropClass);
  }

  if (prevItem.value && prevItem.value !== target) {
    prevItem.value?.classList.remove(props.dropClass);
  }

  prevItem.value = target;
  emit("dragOver", event, index);
};

const handleDrop = (event: DragEvent, index: number) => {
  const draggedIndex = Number(event.dataTransfer!.getData("text/plain"));
  const draggedItem = props.modelValue[draggedIndex];
  emit("drop", event, index);
  let target = event.target as HTMLElement;
  if (props.customDropHandler) {
    props.customDropHandler(startItem.value,startIndex.value,target,index);
  }
  if (props.swap) {
    const newItems = [...props.modelValue];
    newItems[draggedIndex] = props.modelValue[index];
    newItems[index] = draggedItem;
    emit("update:modelValue", newItems);
  } else if (props.reorder) {
    const newItems = [...props.modelValue];
    newItems.splice(draggedIndex, 1);
    newItems.splice(index, 0, draggedItem);
    emit("update:modelValue", newItems);
  }

  //  Clearing the classes
  target?.classList.remove(props.dropClass)
  startItem.value?.classList.remove(props.dragClass);

 
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
