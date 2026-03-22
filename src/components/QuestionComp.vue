<script setup>
defineProps(['question', 'number'])
</script>

<template>
  <section id="question">
    <p class="question-num text-italic-small">Question {{ number + 1 }} of 10</p>
    <p class="question text-preset-3">{{ question }}</p>
  </section>
</template>

<style scoped>
#question {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-200);
}

.question-num {
  color: var(--text-color-light);
}

.question {
  color: var(--text-color-normal);
}
</style>
