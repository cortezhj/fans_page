<script setup lang="ts">
interface SocialItem {
  name: string
  handle: string
  color: string
  iconSrc: string
  link: string
}

const socials: SocialItem[] = [
  {
    name: 'Instagram',
    handle: '@deep_lower',
    color: '#E1306C',
    iconSrc: '/favicon/instagram.png',
    link: 'https://www.instagram.com/deep_lower/?hl=es'
  },
  {
    name: 'Spotify',
    handle: 'DeepLower',
    color: '#1DB954',
    iconSrc: '/favicon/spotify.webp',
    link: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=RmIZcVxeQPW7EF7umwiBtw'
  },
  {
    name: 'YouTube',
    handle: '@Deep_Lower',
    color: '#FF0000',
    iconSrc: '/favicon/youtube.png',
    link: 'https://www.youtube.com/@Deep_Lower/featured'
  },
  {
    name: 'TikTok',
    handle: '@el.deep_lower',
    color: '#010101',
    iconSrc: '/favicon/tiktok.png',
    link: 'https://www.tiktok.com/@el.deep_lower'
  },
  {
    name: 'SoundCloud',
    handle: 'deep-lower',
    color: '#FF5500',
    iconSrc: '/favicon/soundcloud.png',
    link: 'https://soundcloud.com/deep-lower'
  },
  {
    name: 'Facebook',
    handle: 'Deep Lower',
    color: '#1877F2',
    iconSrc: '/favicon/facebook.png',
    link: 'https://www.facebook.com/profile.php?id=100063647709814'
  }
]
</script>

<template>
  <section id="redes" class="social-section section-padding section-white-theme">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">REDES <span class="gradient-text-fire">SOCIALES</span></h2>
        <p class="section-desc">
          Conéctate directamente con DeepLower. Nuevos lanzamientos, ensayos y detrás de cámaras.
        </p>
      </div>

      <!-- Horizontal Social Buttons Grid -->
      <div class="socials-grid">
        <a 
          v-for="item in socials" 
          :key="item.name" 
          :href="item.link" 
          target="_blank" 
          rel="noopener noreferrer" 
          class="social-card"
        >
          <div class="social-icon-box" :style="{ borderColor: item.color }">
            <img :src="item.iconSrc" :alt="item.name" class="social-icon-img" />
          </div>

          <div class="social-info">
            <h3 class="social-name">{{ item.name }}</h3>
            <span class="social-handle">{{ item.handle }}</span>
          </div>

          <span class="social-arrow">↗</span>
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.social-section {
  position: relative;
  background-color: #ffffff;
  color: #09090b;
}

.socials-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

@media (max-width: 992px) {
  .socials-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }
}

@media (max-width: 580px) {
  .socials-grid {
    grid-template-columns: 1fr;
    gap: 12px;
  }
}

.social-card {
  position: relative;
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 16px;
  background: #ffffff;
  border: 1px solid #e4e4e7;
  border-radius: var(--radius-md);
  padding: 14px 20px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.03);
  transition: all var(--transition-smooth);
  text-decoration: none;
}

.social-card:hover {
  transform: translateY(-4px);
  border-color: var(--accent-red);
  box-shadow: 0 8px 24px rgba(239, 68, 68, 0.15);
}

.social-icon-box {
  width: 46px;
  height: 46px;
  min-width: 46px;
  border-radius: 50%;
  border: 2px solid;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f4f4f6;
  transition: transform var(--transition-fast);
}

.social-card:hover .social-icon-box {
  transform: scale(1.08);
}

.social-icon-img {
  width: 24px;
  height: 24px;
  object-fit: contain;
  display: block;
}

.social-info {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-width: 0;
  gap: 2px;
}

.social-name {
  font-size: 1.05rem;
  color: #09090b;
  font-weight: 800;
  line-height: 1.2;
}

.social-handle {
  font-size: 0.85rem;
  color: var(--accent-red);
  font-weight: 700;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.social-arrow {
  color: #a1a1aa;
  font-size: 1.2rem;
  font-weight: 700;
  margin-left: auto;
  transition: transform var(--transition-fast), color var(--transition-fast);
}

.social-card:hover .social-arrow {
  transform: translate(3px, -3px);
  color: var(--accent-red);
}
</style>
