<script setup lang="ts">
const { size = 32 } = defineProps<{ size?: number }>();
</script>

<template>
  <button class="button-icon" :style="{ width: `${size}px`, height: `${size}px` }">
    <slot />
  </button>
</template>

<style scoped>
.button-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--color-fg);
  border-radius: 50%;
  border: none;
  cursor: pointer;
}
.button-icon:hover {
  background: var(--color-fg-hover);
}
</style>
