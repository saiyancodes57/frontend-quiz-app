<script setup>
import htmlIcon from '@/assets/images/icon-html.svg'
import cssIcon from '@/assets/images/icon-css.svg'
import jsIcon from '@/assets/images/icon-js.svg'
import a11yIcon from '@/assets/images/icon-accessibility.svg'

defineProps(['subjects'])
const emit = defineEmits(['subjectChosen'])
const images = {
  HTML: htmlIcon,
  CSS: cssIcon,
  JavaScript: jsIcon,
  Accessibility: a11yIcon,
}

// Emits to App, which sets the stage
function chooseSubject(subject) {
  emit('subjectChosen', subject)
}
</script>

<template>
  <nav aria-label="Quiz subjects">
    <ul>
      <li v-for="subject in subjects" :key="subject">
        <button @click="chooseSubject(subject)" class="text-preset-4">
          <img :src="images[subject]" />
          {{ subject }}
        </button>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

button {
  overflow: hidden;
  background-color: var(--btn-bg-color);
  text-align: left;
  display: flex;
  align-items: center;
  gap: var(--spacing-200);
  color: var(--text-color-normal);
  padding: var(--spacing-200);
  border-radius: 0.75rem;
  border: 3px solid transparent;
  outline: none;
  height: 4.5rem;
  width: 100%;
  box-shadow:
    0 10px 20px rgba(0, 0, 0, 0.08),
    0 2px 6px rgba(0, 0, 0, 0.08);

  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease;
}

button:hover,
button:focus-visible {
  /* Lift the button slightly and deepen the shadow */
  transform: translateY(-2px);
  box-shadow:
    0 15px 30px rgba(0, 0, 0, 0.16),
    0 4px 10px rgba(0, 0, 0, 0.12);
  border-color: var(--purple-600);
}
</style>
