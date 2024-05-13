<script setup lang="ts">
import SortImages from "./components/SortImages.vue";
import SwapImages from "./components/SwapImages.vue";
import SortNumericList from "./components/SortNumericList.vue";
import SwapNumericList from "./components/SwapNumericList.vue";
</script>

<template>
  <main>
    <header class="mb-12">
      <h1 class="text-6xl text-center mt-10">Vue3-drag-n-drop</h1>
    </header>
    <section>
      <h2 class="text-4xl text-left mb-2">Sort</h2>
      <SortImages />
    </section>
    <section>
      <h2 class="text-4xl text-left mb-2 mt-10">Swap</h2>
      <SwapImages />
    </section>
    <div class="flex flex-wrap justify-between">
      <section>
        <h2 class="text-4xl text-left mb-2 mt-10">List Sort</h2>
        <SortNumericList />
      </section>
      <section>
        <h2 class="text-4xl text-left mb-2 mt-10">List Swap</h2>
        <SwapNumericList />
      </section>
    </div>
  </main>
</template>

<style>
.drag-target {
  background-color: rgba(0, 0, 0, 0.1);
  outline: 4px dashed #f56565;
  outline-offset: 4px;
  border-radius: 0.5rem;
  padding: 0.5rem;
}

.drop-target {
  background-color: rgba(0, 0, 0, 0.1);
  outline: 4px dashed #4299e1;
  outline-offset: 4px;
  border-radius: 0.5rem;
  padding: 0.5rem;
}
</style>

