<script setup lang="ts">
import { inject } from 'vue'

interface FriendProfileData {
  Username: string
  Age: string
  Skill: string
  School: string
  Score: number
  ProfilePicture: string
}

defineOptions({
  name: 'FriendProfile'
})

const friendProfile = inject<FriendProfileData[]>('friendProfile')

if (!friendProfile) {
  throw new Error('FriendProfile requires friendProfile to be provided by an ancestor.')
}
</script>

<template>
  <section class="friend-profiles" aria-labelledby="friend-profiles-title">
    <h2 id="friend-profiles-title">Friends</h2>
    <div class="friend-profiles__list">
      <RouterLink
        v-for="profile in friendProfile"
        :key="profile.Username"
        class="friend-profile-link"
        :to="{ name: 'friend-profile', params: { username: profile.Username } }"
      >
        <article class="friend-profile">
          <div class="friend-profile__heading">
          <img
            v-if="profile.ProfilePicture"
            class="friend-profile__picture"
            :src="profile.ProfilePicture"
            :alt="`${profile.Username}'s profile picture`"
          />
          <h3 class="friend-profile__name">{{ profile.Username }}</h3>
          </div>
          <dl class="friend-profile__details">
          <div>
            <dt>Age</dt>
            <dd>{{ profile.Age }}</dd>
          </div>
          <div>
            <dt>Skill</dt>
            <dd>{{ profile.Skill }}</dd>
          </div>
          <div>
            <dt>School</dt>
            <dd>{{ profile.School }}</dd>
          </div>
          <div>
            <dt>Score</dt>
            <dd>{{ profile.Score }}</dd>
          </div>
          </dl>
        </article>
      </RouterLink>
    </div>
  </section>
</template>
