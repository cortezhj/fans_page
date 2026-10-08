<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import AboutBio from './components/AboutBio.vue'
import MusicPlayer from './components/MusicPlayer.vue'
import Gallery from './components/Gallery.vue'
import SocialHub from './components/SocialHub.vue'
import ContactBooking from './components/ContactBooking.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="app-wrapper">
    <Navbar />
    <main>
      <Hero />
      <AboutBio />
      <MusicPlayer />
      <Gallery />
      <SocialHub />
      <ContactBooking />
    </main>
    <Footer />
  </div>
</template>

<style scoped>
.app-wrapper {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
}
</style>
