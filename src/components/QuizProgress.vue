<script setup>
defineProps(['questionNumber'])
</script>

<template>
  <progress min="0" :value="questionNumber" max="10"></progress>
</template>

<style scoped>
progress {
  width: 100%;
  accent-color: var(--purple-600);
}
</style>
