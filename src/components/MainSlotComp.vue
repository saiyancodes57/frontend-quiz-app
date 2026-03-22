<script setup></script>

<template>
  <main>
    <slot></slot>
  </main>
</template>

<style scoped>
main {
  display: grid;
  gap: var(--spacing-500);
  padding: var(--spacing-400) var(--spacing-300);
}

@media (min-width: 48rem) {
  main {
    padding: var(--spacing-800);
  }
}

@media (min-width: 80rem) {
  main {
    padding: var(--spacing-1800);
    gap: var(--spacing-1600);
    grid-template-columns: 1fr 1fr;
  }
}
</style>
