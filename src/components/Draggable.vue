<script setup lang="ts">
const emit = defineEmits([
  "dragStart",
  "dragOver",
  "drop",
  "dragEnd",
  "update:modelValue",
]);

const props = defineProps({
  modelValue: {
    type: Array as () => Array<any>,
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

const resetClasses = (event: DragEvent) => {
  (event.target && props.dropClass) && (event.target as HTMLElement).classList.remove(props.dropClass);
  props.dragClass && startItem.value?.classList.remove(props.dragClass);
  props.dropClass && prevItem.value?.classList.remove(props.dropClass);
};

const handleDragStart = (event: DragEvent, index: number) => {
  event.dataTransfer!.setData("text/plain", index.toString());
  let target = event.target as HTMLElement;
  props.dragClass && target.classList.add(props.dragClass)
  startItem.value = target;
  startIndex.value = index;
  emit("dragStart", event, index);
};

const handleDragOver = (event: DragEvent, index: number) => {
  event.preventDefault();

  if (!props.dropClass) return;

  let target = event.target as HTMLElement;
  if (startItem.value === target) {
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
    props.customDropHandler(startItem.value, startIndex.value, target, index);
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
  resetClasses(event);
};

const handleDragEnd = (event: DragEvent, index: number) => {
  resetClasses(event);
  emit("dragEnd", event, index);
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
          @dragend="handleDragEnd($event, index)"
      >
        <slot :item="item"></slot>
      </div>
    </template>
  </div>
</template>
