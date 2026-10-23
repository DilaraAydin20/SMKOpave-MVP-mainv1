<script setup lang="ts">
import { computed, inject } from 'vue'

interface Profile {
  Username: string
  Score: number
}

const userProfile = inject<Profile>('userProfile')
const friendProfiles = inject<Profile[]>('friendProfile')

if (!userProfile) {
  throw new Error('Leaderboard requires userProfile to be provided by an ancestor.')
}

if (!friendProfiles) {
  throw new Error('Leaderboard requires friendProfile to be provided by an ancestor.')
}

const leaderboard = computed(() =>
  [userProfile, ...friendProfiles]
    .map(({ Username, Score }) => ({ Username, Score }))
    .sort((first, second) => second.Score - first.Score)
)

const totalPoints = computed(() =>
  leaderboard.value.reduce((total, profile) => total + profile.Score, 0)
)

function placeLabel(index: number): string {
  const place = index + 1
  if (place === 1) return '1st'
  if (place === 2) return '2nd'
  if (place === 3) return '3rd'
  return `${place}th`
}
</script>

<template>
  <section class="leaderboard" aria-labelledby="leaderboard-title">
    <h2 id="leaderboard-title">Leaderboard</h2>
    <p class="leaderboard__total">Total points: <strong>{{ totalPoints }}</strong></p>
    <ol class="leaderboard__list">
      <li v-for="(profile, index) in leaderboard" :key="profile.Username">
        <span class="leaderboard__place">{{ placeLabel(index) }} place</span>
        <span class="leaderboard__name">{{ profile.Username }}</span>
        <strong>{{ profile.Score }} points</strong>
      </li>
    </ol>
  </section>
</template>
