<script setup></script>

<template>
  <section id="welcome">
    <h1 class="welcome-header">
      <span class="text-preset-2-light">Welcome to the</span>
      <strong class="text-preset-2-medium">Frontend Quiz!</strong>
    </h1>
    <p class="text-italic-small">Pick a subject to get started.</p>
  </section>
</template>

<style scoped>
h1 {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-50);
}

strong,
span {
  color: var(--text-color-normal);
}

p {
  color: var(--text-color-light);
  margin-top: 1rem;
}
</style>
