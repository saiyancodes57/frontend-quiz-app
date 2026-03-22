<script setup>
import { ref, computed } from 'vue'
import questions from './questions.json'
import MainSlotComp from './components/MainSlotComp.vue'
import WelcomeHeader from './components/WelcomeHeader.vue'
import QuizOptions from './components/QuizOptions.vue'
import QuestionComp from './components/QuestionComp.vue'
import QuestionOptions from './components/QuestionOptions.vue'
import ThemeToggle from './components/ThemeToggle.vue'
import ResultPage from './components/ResultPage.vue'
import QuizProgress from './components/QuizProgress.vue'
import htmlIcon from '@/assets/images/icon-html.svg'
import cssIcon from '@/assets/images/icon-css.svg'
import jsIcon from '@/assets/images/icon-js.svg'
import a11yIcon from '@/assets/images/icon-accessibility.svg'

const imagesObj = {
  HTML: htmlIcon,
  CSS: cssIcon,
  JavaScript: jsIcon,
  Accessibility: a11yIcon,
}

const isDarkMode = ref(false)
const questionsData = questions
const allSubjects = Object.keys(questionsData)
const stage = ref('welcome')
const questionNumber = ref(0)
const score = ref(0)
const quizTopic = ref('')

function setTheme(value) {
  const root = document.documentElement
  if (value) {
    root.setAttribute('data-theme', 'light')
  } else {
    root.setAttribute('data-theme', 'dark')
  }
  isDarkMode.value = !isDarkMode.value
}

// Checks if we're on the welcome screen
const isWelcome = computed(() => stage.value === 'welcome')

// Returns the question based on the questionNumber
const currentQuestion = computed(() => {
  if (stage.value === 'welcome') return null
  return questionsData[stage.value][questionNumber.value]['question']
})

// Returns the choices based on the questionNumber
const currentChoices = computed(() => {
  if (stage.value === 'welcome') return null
  return questionsData[stage.value][questionNumber.value]['choices']
})

// Sets the stage to whatever the user has chosen
function setSubject(subject) {
  stage.value = subject
  quizTopic.value = subject
}

function checkAnswer(userAnswer) {
  if (userAnswer === questionsData[stage.value][questionNumber.value]['answer']) {
    score.value++
  }
}

function nextQuestion() {
  if (questionNumber.value < 9) {
    questionNumber.value++
  } else {
    stage.value = 'complete'
  }
}

function resetQuiz() {
  stage.value = 'welcome'
  score.value = 0
  questionNumber.value = 0
  quizTopic.value = ''
}

const isQuizActive = computed(() => {
  return stage.value !== 'welcome' && stage.value !== 'complete'
})

const headerSubject = computed(() => {
  return isQuizActive.value ? stage.value : null
})

const currentIcon = computed(() => {
  return isQuizActive.value ? imagesObj[stage.value] || null : null
})
</script>

<template>
  <ThemeToggle
    :subject="headerSubject"
    :image="currentIcon"
    :is-dark="isDarkMode"
    @set-theme="setTheme(isDarkMode)"
  />
  <MainSlotComp>
    <template v-if="isWelcome">
      <WelcomeHeader />
      <QuizOptions :subjects="allSubjects" @subject-chosen="setSubject" />
    </template>

    <template v-else-if="stage === 'complete'">
      <ResultPage
        :score="score"
        @reset-quiz="resetQuiz"
        :subject="quizTopic"
        :image="imagesObj[quizTopic]"
      />
    </template>

    <template v-else>
      <div class="top-component">
        <QuestionComp :question="currentQuestion" :number="questionNumber" />
        <QuizProgress :question-number="questionNumber" />
      </div>
      <QuestionOptions
        :choices="currentChoices"
        @submit-answer="checkAnswer"
        @next-question="nextQuestion"
        :key="questionNumber"
        :correct-answer="questionsData[stage][questionNumber]['answer']"
      />
    </template>
  </MainSlotComp>
</template>

<style scoped>
.top-component {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

@media (min-width: 80rem) {
  .top-component {
    gap: 12rem;
  }
}
</style>
