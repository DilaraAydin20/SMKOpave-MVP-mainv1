<script lang="ts">
import { defineComponent } from 'vue'
import UserProfile from '../components/UserProfile.vue'
import FriendProfile from '../components/FriendProfile.vue'
import Streak from '../components/Streak.vue'

export default defineComponent({
  name: 'MyProfile',
  components: {
    UserProfile,
    FriendProfile,
    Streak
  }
})
</script>

<template>
  <section class="my-profile-page" aria-labelledby="my-profile-title">
    <h1 id="my-profile-title">Min profil</h1>
    <UserProfile />
    <Streak />
    <FriendProfile />
  </section>
</template>
