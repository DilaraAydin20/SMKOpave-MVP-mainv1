<script setup lang="ts">
import { inject } from 'vue'

interface UserProfileData {
  Username: string
  Age: string
  Skill: string
  School: string
  Score: number
  ProfilePicture: string
}

defineOptions({
  name: 'UserProfile'
})

const userProfile = inject<UserProfileData>('userProfile')

if (!userProfile) {
  throw new Error('UserProfile requires userProfile to be provided by an ancestor.')
}
</script>

<template>
  <section class="user-profile" aria-label="User profile">
    <img
      v-if="userProfile.ProfilePicture"
      class="user-profile__picture"
      :src="userProfile.ProfilePicture"
      :alt="`${userProfile.Username}'s profile picture`"
    />
    <div class="user-profile__information">
      <h2 class="user-profile__name">{{ userProfile.Username }}</h2>
      <dl class="user-profile__details">
        <div>
          <dt>Age</dt>
          <dd>{{ userProfile.Age }}</dd>
        </div>
        <div>
          <dt>Skill</dt>
          <dd>{{ userProfile.Skill }}</dd>
        </div>
        <div>
          <dt>School</dt>
          <dd>{{ userProfile.School }}</dd>
        </div>
        <div>
          <dt>Score</dt>
          <dd>{{ userProfile.Score }}</dd>
        </div>
      </dl>
    </div>
  </section>
</template>
