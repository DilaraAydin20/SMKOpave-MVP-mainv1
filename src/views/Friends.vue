<script setup lang="ts">
import { computed, inject } from 'vue'
import { useRoute } from 'vue-router'

interface FriendProfileData {
  Username: string
  Age: string
  Skill: string
  School: string
  Score: number
  ProfilePicture: string
}

defineOptions({
  name: 'Friends'
})

const friendProfiles = inject<FriendProfileData[]>('friendProfile')

if (!friendProfiles) {
  throw new Error('Friends requires friendProfile to be provided by an ancestor.')
}

const route = useRoute()
const profile = computed(() => {
  const username = route.params.username
  return typeof username === 'string'
    ? friendProfiles.find((friend) => friend.Username === username)
    : undefined
})
</script>

<template>
  <section class="friend-page" aria-labelledby="friend-page-title">
    <template v-if="profile">
      <h1 id="friend-page-title">{{ profile.Username }}'s profile</h1>
      <article class="friend-profile">
        <img
          v-if="profile.ProfilePicture"
          class="friend-profile__picture"
          :src="profile.ProfilePicture"
          :alt="`${profile.Username}'s profile picture`"
        />
        <div class="friend-profile__information">
          <h2 class="friend-profile__name">{{ profile.Username }}</h2>
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
        </div>
      </article>
    </template>
    <p v-else role="status">Friend profile not found.</p>
  </section>
</template>
