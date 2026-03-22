<script setup>
const emit = defineEmits(['setTheme'])
defineProps(['subject', 'image', 'isDark'])
import iconSunLight from '@/assets/images/icon-sun-light.svg'
import iconSunDark from '@/assets/images/icon-sun-dark.svg'

import iconMoonLight from '@/assets/images/icon-moon-light.svg'
import iconMoonDark from '@/assets/images/icon-moon-dark.svg'

function toggle() {
  emit('setTheme')
}
</script>

<template>
  <header>
    <div class="header-right">
      <img :src="image" :alt="subject" />
      <p class="subject text-preset-4">{{ subject }}</p>
    </div>
    <div class="header-right">
      <img v-if="!isDark" :src="iconSunDark" class="sun-icon" alt="Dark theme sun icon" />
      <img v-else :src="iconSunLight" class="sun-icon" alt="Light theme sun icon" />

      <button class="theme-toggle" :class="{ active: isDark }" @click="toggle">
        <div class="toggle-circle"></div>
      </button>
      <img v-if="!isDark" :src="iconMoonDark" class="moon-icon" alt="Dark theme moon icon" />
      <img v-else :src="iconMoonLight" class="moon-icon" alt="Light theme moon icon" />
    </div>
  </header>
</template>

<style scoped>
header {
  min-height: 4.5rem;
  padding: var(--spacing-200) var(--spacing-300);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-right {
  display: flex;
  align-items: center;
  gap: var(--spacing-300);
}

.subject {
  color: var(--text-color-normal);
}

.theme-toggle {
  background-color: var(--purple-600);
  width: 2rem;
  height: 1.25rem;
  padding: var(--spacing-50);
  display: flex;
  align-items: center;
  border: none;
  border-radius: 999px;
}

.toggle-circle {
  width: 0.75rem;
  height: 0.75rem;
  background-color: var(--white);
  border-radius: 100%;
  transition: transform 0.2s ease;
}

.theme-toggle.active .toggle-circle {
  transform: translateX(0.75rem);
}

@media (min-width: 48rem) {
  header {
    padding: var(--spacing-400) var(--spacing-800);
  }
}

@media (min-width: 80rem) {
  header {
    padding: var(--spacing-400) var(--spacing-1800);
  }
}
</style>
