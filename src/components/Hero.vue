<script setup lang="ts">
const platforms = [
  { name: 'Spotify', iconSrc: '/favicon/spotify.webp', link: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA' },
  { name: 'YouTube', iconSrc: '/favicon/youtube.png', link: 'https://www.youtube.com/@Deep_Lower/featured' },
  { name: 'SoundCloud', iconSrc: '/favicon/soundcloud.png', link: 'https://soundcloud.com/deep-lower' },
]
</script>

<template>
  <section id="inicio" class="hero-section">
    <!-- Background Image & Cinematic Overlays -->
    <div class="hero-bg-container">
      <img src="/images/hero.jpg" alt="DeepLower en concierto" class="hero-bg-img" />
      <div class="hero-overlay-gradient"></div>
      <div class="hero-overlay-radial"></div>
      <div class="hero-noise"></div>
    </div>

    <div class="hero-content">
      <!-- Tag / New Release Badge -->
      <div class="hero-badge-wrap">
        <div class="hero-badge">
          <span class="badge-pulse"></span>
          <span class="badge-text">NUEVO SENCILLO DISPONIBLE:</span>
          <span class="badge-track">"DAME UN CHANCE"</span>
        </div>
      </div>

      <!-- Main Titles -->
      <h1 class="hero-title">
        <span class="title-deep">DEEP</span><span class="title-deep">LOWER</span>
      </h1>

      <!-- CTA Action Buttons -->
      <div class="hero-actions">
        <a href="#musica" class="btn btn-red hero-btn">
          <span class="btn-icon">▶</span>
          <span>Escuchar Éxitos</span>
        </a>
      </div>

      <!-- Streaming Platforms Links -->
      <div class="hero-streaming">
        <span class="streaming-label">Disponible en plataformas:</span>
        <div class="streaming-pills">
          <a 
            v-for="platform in platforms" 
            :key="platform.name" 
            :href="platform.link" 
            target="_blank" 
            rel="noopener noreferrer"
            class="platform-pill"
          >
            <img :src="platform.iconSrc" :alt="platform.name" class="platform-icon-img" />
            <span>{{ platform.name }}</span>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 80px 20px 40px;
  overflow: hidden;
  box-sizing: border-box;
}

.hero-bg-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.hero-bg-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 20%;
  filter: brightness(0.98) contrast(1.12);
}

.hero-overlay-gradient {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.38) 0%,
    rgba(0, 0, 0, 0.45) 55%,
    rgba(0, 0, 0, 0.92) 100%
  );
}

.hero-overlay-radial {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    circle at center,
    rgba(239, 68, 68, 0.08) 0%,
    transparent 65%
  );
}

.hero-noise {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(rgba(255, 255, 255, 0.04) 1px, transparent 0);
  background-size: 28px 28px;
  opacity: 0.2;
}

.hero-content {
  position: relative;
  z-index: 10;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  max-width: 950px;
  margin: 0 auto;
}

.hero-badge-wrap {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-bottom: 24px;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 8px 22px;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(239, 68, 68, 0.55);
  border-radius: var(--radius-full);
  box-shadow: 0 0 24px rgba(239, 68, 68, 0.3);
}

.badge-pulse {
  width: 8px;
  height: 8px;
  background-color: var(--accent-red);
  border-radius: 50%;
  box-shadow: 0 0 10px var(--accent-red);
  animation: pulse 1.8s infinite;
  flex-shrink: 0;
}

@keyframes pulse {
  0% { transform: scale(0.9); opacity: 0.8; }
  50% { transform: scale(1.4); opacity: 1; box-shadow: 0 0 16px var(--accent-red); }
  100% { transform: scale(0.9); opacity: 0.8; }
}

.badge-text {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: #fff;
  text-transform: uppercase;
}

.badge-track {
  font-size: 0.78rem;
  font-weight: 800;
  color: var(--accent-red);
}

.hero-title {
  font-family: var(--font-display);
  font-size: clamp(2.1rem, 7.5vw, 6.2rem);
  font-weight: 800;
  letter-spacing: 0.04em;
  line-height: 1.05;
  margin: 0 auto 28px;
  text-transform: uppercase;
  text-align: center;
  width: 100%;
  white-space: nowrap;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.16em;
  filter: drop-shadow(0 6px 18px rgba(0, 0, 0, 0.95));
}

@media (max-width: 480px) {
  .hero-title {
    font-size: clamp(1.85rem, 8.2vw, 2.6rem);
    letter-spacing: 0.02em;
    gap: 0.12em;
  }
}

.title-deep {
  color: #ffffff;
  display: inline-block;
  text-shadow: 0 0 25px rgba(255, 255, 255, 0.25);
}

.title-lower {
  color: #ef4444;
  display: inline-block;
  text-shadow: 0 0 24px rgba(239, 68, 68, 0.8), 0 0 45px rgba(239, 68, 68, 0.35);
}

.hero-actions {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 36px;
}

.hero-btn {
  padding: 16px 44px;
  font-size: 1.05rem;
}

.hero-streaming {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 14px;
}

.streaming-label {
  font-size: 0.82rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: rgba(255, 255, 255, 0.75);
  font-weight: 600;
  text-align: center;
}

.streaming-pills {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.platform-pill {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 10px 22px;
  background: rgba(0, 0, 0, 0.45);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: var(--radius-full);
  font-size: 0.88rem;
  font-weight: 600;
  color: #ffffff;
  transition: all var(--transition-fast);
}

.platform-pill:hover {
  background: rgba(239, 68, 68, 0.15);
  border-color: var(--accent-red);
  color: #fff;
  transform: translateY(-2px);
  box-shadow: 0 4px 14px rgba(239, 68, 68, 0.3);
}

.platform-icon-img {
  width: 20px;
  height: 20px;
  object-fit: contain;
  display: block;
}
</style>
