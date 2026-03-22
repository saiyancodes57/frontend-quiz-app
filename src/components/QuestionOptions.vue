<script setup>
import { ref } from 'vue'
import iconCorrect from '@/assets/images/icon-correct.svg'
import iconIncorrect from '@/assets/images/icon-incorrect.svg'
const props = defineProps(['choices', 'correctAnswer'])
const emit = defineEmits(['submitAnswer', 'nextQuestion'])

const selected = ref('')
const submitted = ref(false)
const options = ['A', 'B', 'C', 'D']

function selectAnswer(answer) {
  selected.value = answer
}

function submitAnswer() {
  if (selected.value !== '') {
    emit('submitAnswer', selected.value)
    submitted.value = true
  }
}

function nextQuestion() {
  emit('nextQuestion')
}

function classObject(answer) {
  return {
    selected: selected.value === answer,
    correct: submitted.value && answer === props.correctAnswer,
    incorrect:
      submitted.value && answer === selected.value && selected.value !== props.correctAnswer,
  }
}
</script>

<template>
  <nav aria-label="Possible choices">
    <ul>
      <li v-for="(answer, index) in choices" :key="answer">
        <button :class="classObject(answer)" @click="selectAnswer(answer)" :disabled="submitted">
          <div class="letter text-preset-4">{{ options[index] }}</div>
          <span class="answer text-preset-4">{{ answer }}</span>
          <img v-if="submitted && answer === correctAnswer" :src="iconCorrect" alt="Correct icon" />
          <img
            v-if="submitted && answer === selected && selected !== correctAnswer"
            :src="iconIncorrect"
            alt="Incorrect icon"
          />
        </button>
      </li>
    </ul>
    <button
      v-if="!submitted"
      class="submit text-preset-4"
      type="button"
      @click="submitAnswer"
      :disabled="!selected"
    >
      Submit Answer
    </button>
    <button v-else class="submit text-preset-4" type="button" @click="nextQuestion">
      Next Question
    </button>
  </nav>
</template>

<style scoped>
ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.answer {
  color: var(--text-color-normal);
}

button {
  word-break: break-all;
  text-align: left;
  padding: var(--spacing-200);
  width: 100%;
  display: flex;
  align-items: center;
  gap: var(--spacing-200);
  border-radius: 0.75rem;
  background-color: var(--btn-bg-color);
  border: 3px solid transparent;
  outline: none;
  box-shadow:
    0 10px 20px rgba(0, 0, 0, 0.08),
    0 2px 6px rgba(0, 0, 0, 0.08);

  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease;
}

button span {
  flex: 1; /* This tells the text to take up all remaining space */
  word-break: break-word; /* Ensures long words don't break the layout */
}

button:not(:disabled):hover,
button:not(:disabled):focus-visible {
  /* Lift the button slightly and deepen the shadow */
  transform: translateY(-2px);
  box-shadow:
    0 15px 30px rgba(0, 0, 0, 0.16),
    0 4px 10px rgba(0, 0, 0, 0.12);
  border-color: var(--purple-600);
}

.submit {
  margin-top: 1rem;
  height: 4.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--purple-600);
  color: var(--white);
  transition:
    filter 0.2s ease,
    transform 0.2s ease;
}

.submit:not(:disabled):hover,
.submit:not(:disabled):focus-visible {
  /* Filter makes the purple 20%  */
  filter: brightness(1.2);
  transform: translateY(-2px);
  box-shadow: 0px 10px 20px color-mix(in srgb, var(--purple-600), transparent 20%);
}

.submit:active {
  /* Makes it look "pressed" by darkening it */
  filter: brightness(0.8);
  transform: translateY(0);
}

.selected {
  border-color: var(--purple-600);
}

.letter {
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--grey-50);
  color: var(--text-color-light);
  font-weight: 600;
  border-radius: 0.5rem;
}

button:disabled {
  background-color: var(--purple-100);
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

.correct {
  border-color: var(--green-500);
}

.incorrect {
  border-color: var(--red-500);
}

.incorrect > .letter {
  background-color: var(--red-500);
  color: var(--white);
}

.correct > .letter {
  background-color: var(--green-500);
  color: var(--white);
}

@media (min-width: 40rem) {
  .submit {
    margin-top: 2rem;
  }
}
</style>
