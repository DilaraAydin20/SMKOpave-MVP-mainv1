<template>
  <header class="site-header">
    <div class="site-header__inner">
      <RouterLink class="site-brand" to="/" aria-label="SMK Art Hunt – startside">
        <img src="/brand/smk-logo.svg" alt="" width="92" height="30">
        <span class="site-brand__name">Art Hunt</span>
      </RouterLink>
      <nav class="site-navigation" aria-label="Hovednavigation">
        <RouterLink to="/">Start</RouterLink>
        <RouterLink to="/art-cards">Kunstkort</RouterLink>
        <RouterLink to="/collection">Min samling</RouterLink>
        <RouterLink to="/achievements">Achievements</RouterLink>
        <RouterLink to="/my-profile">Min profil</RouterLink>
        <RouterLink to="/scoreboard">Scoreboard</RouterLink>
      </nav>
    </div>
  </header>
</template>
