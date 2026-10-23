<script setup lang="ts">
import { computed, inject } from 'vue'

interface SchoolScore {
  School: string
  Score: number
}

const tournamentScores = inject<SchoolScore[]>('tournamentScores')

if (!tournamentScores) {
  throw new Error('Tournament requires tournamentScores to be provided by an ancestor.')
}

const rankedSchools = computed(() =>
  [...tournamentScores].sort((first, second) => second.Score - first.Score)
)
</script>

<template>
  <section class="tournament" aria-labelledby="tournament-title">
    <h2 id="tournament-title">Tournament</h2>
    <ol class="tournament__list">
      <li v-for="school in rankedSchools" :key="school.School">
        <span>{{ school.School }}</span>
        <strong>{{ school.Score }} points</strong>
      </li>
    </ol>
  </section>
</template>
