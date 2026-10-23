<script lang="ts">
import { defineComponent, ref } from 'vue'

type Theme = 'light' | 'dark'

const themeStorageKey = 'smk-art-hunt-theme'

export default defineComponent({
  name: 'Header',
  setup() {
    const storedTheme = window.localStorage.getItem(themeStorageKey)
    const theme = ref<Theme>(storedTheme === 'dark' ? 'dark' : 'light')

    document.documentElement.dataset.theme = theme.value

    function toggleTheme() {
      const nextTheme = theme.value === 'dark' ? 'light' : 'dark'
      window.localStorage.setItem(themeStorageKey, nextTheme)
      theme.value = nextTheme
      document.documentElement.dataset.theme = nextTheme
    }

    return { theme, toggleTheme }
  }
})
</script>

<template>
  <header class="site-header">
    <div class="site-header__inner">
      <RouterLink class="site-brand" to="/" aria-label="SMK Art Hunt – startside">
        <img src="/brand/smk-logo.svg" alt="" width="92" height="30">
        <span class="site-brand__name">Art Hunt</span>
      </RouterLink>
      <div class="site-header__tools">
        <nav class="site-navigation" aria-label="Hovednavigation">
          <RouterLink to="/">Start</RouterLink>
          <RouterLink to="/art-cards">Kunstkort</RouterLink>
          <RouterLink to="/collection">Min samling</RouterLink>
          <RouterLink to="/achievements">Achievements</RouterLink>
          <RouterLink to="/my-profile">Min profil</RouterLink>
          <RouterLink to="/scoreboard">Scoreboard</RouterLink>
        </nav>
        <button
          class="theme-toggle"
          type="button"
          :aria-label="theme === 'dark' ? 'Skift til lyst tema' : 'Skift til mørkt tema'"
          :aria-pressed="theme === 'dark'"
          @click="toggleTheme"
        >
          {{ theme === 'dark' ? 'Lyst tema' : 'Mørkt tema' }}
        </button>
      </div>
    </div>
  </header>
</template>
