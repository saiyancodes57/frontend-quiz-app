<script setup>
defineProps(['score', 'image', 'subject'])
const emit = defineEmits(['resetQuiz'])

function resetQuizApp() {
  emit('resetQuiz')
}
</script>

<template>
  <header>
    <p class="text-preset-2-light">Quiz completed</p>
    <h1 class="text-preset-2-medium">You scored...</h1>
  </header>
  <div class="bottom-container">
    <section class="test-score">
      <div class="test-topic">
        <img :src="image" alt="Subject icon" />
        <p class="topic text-preset-4">{{ subject }}</p>
      </div>
      <p class="score text-preset-1">{{ score }}</p>
      <p class="total text-preset-4">out of 10</p>
    </section>
    <button class="submit text-preset-4 play-again" @click="resetQuizApp" type="button">
      Play Again
    </button>
  </div>
</template>

<style scoped>
header {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-100);
}

header > p,
header > h1,
.topic,
.score {
  color: var(--text-color-normal);
}

.total {
  color: var(--text-color-light);
}

.test-score {
  padding: var(--spacing-400);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-200);
  background-color: var(--btn-bg-color);
  border-radius: 0.75rem;

  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.08);
}

.test-topic {
  display: flex;
  align-items: center;
  gap: var(--spacing-200);
}

button {
  margin-top: var(--spacing-200);
  padding: var(--spacing-200);
  color: var(--white);
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-200);
  border-radius: 0.75rem;
  background-color: var(--purple-600);
  border: 3px solid transparent;
  outline: none;
  box-shadow:
    0 10px 20px rgba(0, 0, 0, 0.08),
    0 2px 6px rgba(0, 0, 0, 0.08);

  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease;
}
</style>
