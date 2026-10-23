<script lang="ts">
import { defineComponent } from 'vue'
import Events from '../components/Events.vue'
import { artworks } from '../data/artworks'

export default defineComponent({
  name: 'HomeView',
  components: {
    Events
  },
  data() {
    return {
      gameName: 'Kunstjagt på SMK',
      featuredArtwork: artworks[0]
    }
  }
})
</script>

<template>
  <section class="home-page" aria-labelledby="home-title">
    <div class="home-hero">
      <div class="home-hero__copy">
        <p class="eyebrow">SMK · Kunstjagt</p>
        <h1 id="home-title">{{ gameName }}</h1>
        <p class="home-hero__intro">Et lille spil om at gå på opdagelse i kunsten.</p>
        <div class="home-hero__actions">
          <RouterLink class="primary-action" to="/art-cards">Gå på kunstjagt</RouterLink>
          <RouterLink class="text-action" to="/collection">Se min samling <span aria-hidden="true">→</span></RouterLink>
        </div>
        <p class="home-hero__note">15 kunstværker · Nye udfordringer hver dag</p>
      </div>
      <figure class="home-hero__artwork">
        <img :src="featuredArtwork.imageUrl" :alt="featuredArtwork.imageAlt">
        <figcaption>
          <span class="eyebrow">Et værk fra samlingen</span>
          <strong>{{ featuredArtwork.title }}</strong>
          <span>{{ featuredArtwork.artist }} · {{ featuredArtwork.productionPeriod }}</span>
        </figcaption>
      </figure>
    </div>
    <Events />
  </section>
</template>
