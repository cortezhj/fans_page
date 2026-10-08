<script setup lang="ts">
import { ref, computed, onUnmounted } from 'vue'

interface Track {
  id: number
  title: string
  album: string
  year: string
  duration: string
  durationSec: number
  cover: string
  genre: string
  audioSrc: string
  spotifyUrl: string
}

const tracks = ref<Track[]>([
  {
    id: 1,
    title: 'Dame Un Chance',
    album: 'Single Oficial',
    year: '2026',
    duration: '4:52',
    durationSec: 292,
    cover: '/music/dame un chance.avif',
    genre: 'Trap Urbano',
    audioSrc: '/music/DEEP LOWER - DAME UN CHANCE.mp3',
    spotifyUrl: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA'
  },
  {
    id: 2,
    title: 'Frenesí',
    album: 'Single Oficial',
    year: '2026',
    duration: '3:06',
    durationSec: 186,
    cover: '/music/frenesi.avif',
    genre: 'Trap / Rap',
    audioSrc: '/music/Deep Lower - FRENESI.mp3',
    spotifyUrl: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA'
  },
  {
    id: 3,
    title: 'Bando',
    album: 'Single Oficial',
    year: '2026',
    duration: '5:46',
    durationSec: 346,
    cover: '/music/bando.avif',
    genre: 'Dark Trap',
    audioSrc: '/music/Deep Lower BANDO.mp3',
    spotifyUrl: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA'
  },
  {
    id: 4,
    title: 'Flow My Way',
    album: 'Single Oficial',
    year: '2026',
    duration: '4:21',
    durationSec: 261,
    cover: '/music/flowmyway.webp',
    genre: 'Trap Flow',
    audioSrc: '/music/Deep Lower Flow My Way.mp3',
    spotifyUrl: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA'
  },
  {
    id: 5,
    title: 'Límites',
    album: 'Single Oficial',
    year: '2026',
    duration: '5:25',
    durationSec: 325,
    cover: '/music/limites.avif',
    genre: 'Hardcore Trap',
    audioSrc: '/music/Deep Lower LIMITES.mp3',
    spotifyUrl: 'https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA'
  }
])

const currentTrackIndex = ref(0)
const isPlaying = ref(false)
const currentTime = ref(0)
const volume = ref(0.8)

let audio: HTMLAudioElement | null = null

const currentTrack = computed(() => tracks.value[currentTrackIndex.value])

const formatTime = (seconds: number) => {
  if (isNaN(seconds) || seconds < 0) return '0:00'
  const mins = Math.floor(seconds / 60)
  const secs = Math.floor(seconds % 60)
  return `${mins}:${secs < 10 ? '0' : ''}${secs}`
}

const initAudio = () => {
  if (!audio && typeof window !== 'undefined') {
    audio = new Audio(currentTrack.value.audioSrc)
    audio.volume = volume.value

    audio.addEventListener('timeupdate', () => {
      if (audio) {
        currentTime.value = Math.floor(audio.currentTime)
      }
    })

    audio.addEventListener('loadedmetadata', () => {
      if (audio && audio.duration && !isNaN(audio.duration) && isFinite(audio.duration)) {
        currentTrack.value.durationSec = Math.floor(audio.duration)
        currentTrack.value.duration = formatTime(Math.floor(audio.duration))
      }
    })

    audio.addEventListener('ended', () => {
      nextTrack()
    })

    audio.addEventListener('play', () => {
      isPlaying.value = true
    })

    audio.addEventListener('pause', () => {
      isPlaying.value = false
    })
  }
}

const togglePlay = () => {
  initAudio()
  if (isPlaying.value) {
    pauseTrack()
  } else {
    playTrack()
  }
}

const playTrack = () => {
  initAudio()
  if (audio) {
    const rawTarget = currentTrack.value.audioSrc
    if (!audio.src.includes(encodeURI(rawTarget.replace(/^\//, '')))) {
      audio.src = rawTarget
      audio.currentTime = currentTime.value
    }
    audio.play().then(() => {
      isPlaying.value = true
    }).catch(err => {
      console.warn('Playback error:', err)
    })
  }
}

const pauseTrack = () => {
  if (audio) {
    audio.pause()
    isPlaying.value = false
  }
}

const selectTrack = (index: number) => {
  currentTrackIndex.value = index
  currentTime.value = 0
  initAudio()
  if (audio) {
    audio.src = currentTrack.value.audioSrc
    audio.currentTime = 0
  }
  playTrack()
}

const nextTrack = () => {
  currentTrackIndex.value = (currentTrackIndex.value + 1) % tracks.value.length
  currentTime.value = 0
  if (audio) {
    audio.src = currentTrack.value.audioSrc
    audio.currentTime = 0
  }
  if (isPlaying.value) {
    playTrack()
  }
}

const prevTrack = () => {
  currentTrackIndex.value = (currentTrackIndex.value - 1 + tracks.value.length) % tracks.value.length
  currentTime.value = 0
  if (audio) {
    audio.src = currentTrack.value.audioSrc
    audio.currentTime = 0
  }
  if (isPlaying.value) {
    playTrack()
  }
}

const seekTrack = (event: Event) => {
  const target = event.target as HTMLInputElement
  const newTime = Number(target.value)
  currentTime.value = newTime
  if (audio) {
    audio.currentTime = newTime
  }
}

const updateVolume = () => {
  if (audio) {
    audio.volume = volume.value
  }
}

onUnmounted(() => {
  if (audio) {
    audio.pause()
    audio.src = ''
    audio = null
  }
})
</script>

<template>
  <section id="musica" class="music-section section-padding">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">LOS MEJORES <span class="gradient-text-fire">TEMAS</span></h2>
        <p class="section-desc">
          Escucha la selección oficial de temas de DeepLower. Dale play para sentir el ritmo.
        </p>
      </div>

      <!-- Main Music Player Console -->
      <div class="player-container glass-card">
        <div class="player-grid">
          <!-- Current Track Artwork & Active Visualizer -->
          <div class="player-art-wrap">
            <div class="album-cover-box" :class="{ 'is-playing': isPlaying }">
              <img :src="currentTrack.cover" :alt="currentTrack.title" class="album-art" />
              <div class="album-glow"></div>
              
              <!-- Floating Equalizer on cover -->
              <div class="cover-equalizer" v-if="isPlaying">
                <span class="eq-bar"></span>
                <span class="eq-bar"></span>
                <span class="eq-bar"></span>
                <span class="eq-bar"></span>
              </div>
            </div>

            <!-- Current Playing Info -->
            <div class="now-playing-info">
              <span class="now-playing-tag">REPRODUCIENDO AHORA</span>
              <h3 class="track-title-main">{{ currentTrack.title }}</h3>
              <p class="track-artist-main">DeepLower</p>
            </div>

            <!-- Interactive Player Controls -->
            <div class="player-controls-box">
              <!-- Progress Bar -->
              <div class="progress-wrap">
                <span class="time-label">{{ formatTime(currentTime) }}</span>
                <div class="slider-container">
                  <input 
                    type="range" 
                    min="0" 
                    :max="currentTrack.durationSec" 
                    :value="currentTime" 
                    @input="seekTrack"
                    class="time-slider"
                  />
                  <div 
                    class="slider-fill" 
                    :style="{ width: `${(currentTime / (currentTrack.durationSec || 1)) * 100}%` }"
                  ></div>
                </div>
                <span class="time-label">{{ currentTrack.duration }}</span>
              </div>

              <!-- Buttons -->
              <div class="control-buttons">
                <button class="ctrl-btn" @click="prevTrack" title="Tema Anterior" aria-label="Canción anterior">
                  ⏮
                </button>
                <button 
                  class="play-main-btn" 
                  @click="togglePlay" 
                  :title="isPlaying ? 'Pausar' : 'Reproducir'"
                  :aria-label="isPlaying ? 'Pausar' : 'Reproducir'"
                >
                  <span v-if="!isPlaying" class="play-icon">▶</span>
                  <span v-else class="pause-icon">⏸</span>
                </button>
                <button class="ctrl-btn" @click="nextTrack" title="Siguiente Tema" aria-label="Siguiente canción">
                  ⏭
                </button>
              </div>

              <!-- Volume Control -->
              <div class="volume-box">
                <span class="volume-icon">🔊</span>
                <input 
                  type="range" 
                  min="0" 
                  max="1" 
                  step="0.05" 
                  v-model.number="volume" 
                  @input="updateVolume"
                  class="volume-slider" 
                  title="Volumen"
                />
              </div>

              <div class="synth-indicator">
                <span class="synth-dot" :class="{ active: isPlaying }"></span>
                <span>{{ isPlaying ? 'Reproduciendo audio oficial' : 'Listo para reproducir' }}</span>
              </div>
            </div>
          </div>

          <!-- Tracks Playlist -->
          <div class="playlist-wrap">
            <div class="playlist-header">
              <span class="col-num">#</span>
              <span class="col-title">TÍTULO</span>
              <span class="col-time">DURACIÓN</span>
            </div>

            <div class="tracks-list">
              <div 
                v-for="(track, index) in tracks" 
                :key="track.id"
                class="track-item"
                :class="{ 'active': currentTrackIndex === index }"
                @click="selectTrack(index)"
              >
                <div class="col-num">
                  <span v-if="currentTrackIndex === index && isPlaying" class="track-playing-icon">
                    <span class="eq-bar"></span>
                    <span class="eq-bar"></span>
                    <span class="eq-bar"></span>
                  </span>
                  <span v-else>{{ index + 1 }}</span>
                </div>

                <div class="col-title track-info-cell">
                  <img :src="track.cover" :alt="track.title" class="track-thumb" />
                  <div>
                    <h4 class="track-name">{{ track.title }}</h4>
                    <span class="track-artist-sub">DeepLower</span>
                  </div>
                </div>

                <div class="col-time track-duration-cell">
                  <span>{{ track.duration }}</span>
                </div>
              </div>
            </div>

            <!-- Streaming Links Banner -->
            <div class="streaming-hub-banner">
              <div class="hub-text">
                <strong>¿Quieres escuchar en tu plataforma favorita?</strong>
                <span>Sigue el perfil oficial de DeepLower:</span>
              </div>
              <div class="hub-buttons">
                <a href="https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=1ldNLxAbSnynVRu0pvcNmA" target="_blank" rel="noopener noreferrer" class="btn btn-transparent btn-sm">
                  <img src="/favicon/spotify.webp" alt="Spotify" class="hub-icon-img" />
                  <span>Spotify</span>
                </a>
                <a href="https://www.youtube.com/@Deep_Lower/featured" target="_blank" rel="noopener noreferrer" class="btn btn-transparent btn-sm">
                  <img src="/favicon/youtube.png" alt="YouTube" class="hub-icon-img" />
                  <span>YouTube</span>
                </a>
                <a href="https://soundcloud.com/deep-lower" target="_blank" rel="noopener noreferrer" class="btn btn-transparent btn-sm">
                  <img src="/favicon/soundcloud.png" alt="SoundCloud" class="hub-icon-img" />
                  <span>SoundCloud</span>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.music-section {
  position: relative;
  background-color: var(--bg-dark);
}

.player-container {
  padding: 36px;
  background: var(--bg-glass-dark);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-lg);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
  width: 100%;
  max-width: 100%;
  box-sizing: border-box;
  overflow: hidden;
}

.player-grid {
  display: grid;
  grid-template-columns: 360px minmax(0, 1fr);
  gap: 40px;
  align-items: start;
  width: 100%;
}

@media (max-width: 1024px) {
  .player-grid {
    grid-template-columns: minmax(0, 1fr);
    gap: 30px;
  }
}

@media (max-width: 600px) {
  .player-container {
    padding: 18px 12px;
    border-radius: var(--radius-md);
  }
  .player-art-wrap {
    padding: 18px 12px;
  }
  .album-cover-box {
    width: min(190px, 58vw);
    height: min(190px, 58vw);
  }
}

@media (max-width: 380px) {
  .player-container {
    padding: 14px 8px;
  }
  .player-art-wrap {
    padding: 14px 8px;
  }
}

/* Left Art & Controls Column */
.player-art-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-lg);
  padding: 28px 24px;
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
}

.album-cover-box {
  position: relative;
  width: 220px;
  height: 220px;
  max-width: 100%;
  border-radius: var(--radius-md);
  margin-bottom: 22px;
}

.album-art {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: var(--radius-md);
  position: relative;
  z-index: 2;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.8);
}

.album-glow {
  position: absolute;
  inset: -10px;
  background: radial-gradient(circle, var(--accent-red-glow), transparent 70%);
  filter: blur(16px);
  z-index: 1;
  opacity: 0.5;
  transition: opacity var(--transition-smooth);
}

.album-cover-box.is-playing .album-glow {
  opacity: 0.9;
  animation: pulse 2.5s infinite alternate;
}

.cover-equalizer {
  position: absolute;
  bottom: 12px;
  right: 12px;
  z-index: 3;
  display: flex;
  gap: 3px;
  align-items: flex-end;
  background: rgba(0, 0, 0, 0.8);
  border: 1px solid rgba(239, 68, 68, 0.3);
  padding: 6px 10px;
  border-radius: var(--radius-sm);
  backdrop-filter: blur(6px);
}

.eq-bar {
  width: 3px;
  background: var(--accent-red);
  border-radius: 2px;
  animation: eqBounce 1.2s infinite ease-in-out;
}

.eq-bar:nth-child(1) { height: 12px; animation-delay: 0.1s; }
.eq-bar:nth-child(2) { height: 18px; animation-delay: 0.3s; }
.eq-bar:nth-child(3) { height: 8px;  animation-delay: 0.2s; }
.eq-bar:nth-child(4) { height: 15px; animation-delay: 0.4s; }

@keyframes eqBounce {
  0%, 100% { transform: scaleY(0.3); }
  50% { transform: scaleY(1); }
}

.now-playing-tag {
  font-size: 0.72rem;
  letter-spacing: 0.15em;
  color: var(--accent-red);
  font-weight: 700;
  display: block;
  margin-bottom: 6px;
}

.now-playing-info {
  width: 100%;
  min-width: 0;
}

.track-title-main {
  font-size: 1.35rem;
  color: #fff;
  margin-bottom: 4px;
  word-break: break-word;
  overflow-wrap: break-word;
}

.track-artist-main {
  font-size: 0.92rem;
  color: var(--text-muted);
  font-weight: 500;
  margin-bottom: 22px;
}

.player-controls-box {
  width: 100%;
  min-width: 0;
}

.progress-wrap {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 18px;
  width: 100%;
  min-width: 0;
}

.time-label {
  font-size: 0.75rem;
  color: var(--text-dim);
  font-weight: 600;
  font-variant-numeric: tabular-nums;
  width: 32px;
  flex-shrink: 0;
}

.slider-container {
  position: relative;
  flex: 1;
  min-width: 0;
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 4px;
  display: flex;
  align-items: center;
}

.time-slider {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
  z-index: 5;
}

.slider-fill {
  height: 100%;
  background: linear-gradient(90deg, #b91c1c, #ef4444);
  box-shadow: 0 0 10px rgba(239, 68, 68, 0.5);
  border-radius: 4px;
  pointer-events: none;
}

.control-buttons {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin-bottom: 18px;
}

.ctrl-btn {
  font-size: 1.4rem;
  color: var(--text-muted);
  transition: all var(--transition-fast);
  padding: 6px;
  background: none;
  border: none;
  cursor: pointer;
}

.ctrl-btn:hover {
  color: #fff;
  transform: scale(1.15);
}

.play-main-btn {
  width: 58px;
  height: 58px;
  border-radius: 50%;
  background: linear-gradient(135deg, #ef4444, #991b1b);
  border: none;
  cursor: pointer;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.3rem;
  box-shadow: 0 4px 20px var(--accent-red-glow);
  transition: all var(--transition-smooth);
}

.play-main-btn:hover {
  transform: scale(1.08);
  box-shadow: 0 6px 28px rgba(239, 68, 68, 0.7);
}

.play-icon {
  margin-left: 3px;
}

.volume-box {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-bottom: 12px;
}

.volume-icon {
  font-size: 0.9rem;
}

.volume-slider {
  width: 100px;
  accent-color: var(--accent-red);
  height: 4px;
  cursor: pointer;
}

.synth-indicator {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  font-size: 0.7rem;
  color: var(--text-dim);
  margin-top: 10px;
}

.synth-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #52525b;
}

.synth-dot.active {
  background: var(--accent-red);
  box-shadow: 0 0 8px var(--accent-red);
}

/* Playlist Table */
.playlist-wrap {
  display: flex;
  flex-direction: column;
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
}

.playlist-header {
  display: grid;
  grid-template-columns: 36px minmax(0, 1fr) 60px;
  padding: 10px 14px;
  gap: 12px;
  font-size: 0.75rem;
  font-weight: 700;
  color: var(--text-dim);
  border-bottom: 1px solid var(--border-subtle);
  letter-spacing: 0.08em;
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
}

.col-time {
  text-align: right;
}

@media (max-width: 640px) {
  .playlist-header {
    grid-template-columns: 28px minmax(0, 1fr) 50px;
    padding: 8px 8px;
    gap: 8px;
  }
}

@media (max-width: 380px) {
  .playlist-header {
    grid-template-columns: 22px minmax(0, 1fr) 44px;
    padding: 8px 4px;
    gap: 6px;
    font-size: 0.7rem;
  }
}

.tracks-list {
  display: flex;
  flex-direction: column;
  gap: 4px;
  margin-top: 8px;
  width: 100%;
  min-width: 0;
}

.track-item {
  display: grid;
  grid-template-columns: 36px minmax(0, 1fr) 60px;
  align-items: center;
  padding: 12px 14px;
  gap: 12px;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all var(--transition-fast);
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
}

@media (max-width: 640px) {
  .track-item {
    grid-template-columns: 28px minmax(0, 1fr) 50px;
    padding: 10px 8px;
    gap: 8px;
  }
}

@media (max-width: 380px) {
  .track-item {
    grid-template-columns: 22px minmax(0, 1fr) 44px;
    padding: 8px 4px;
    gap: 6px;
  }
}

.track-item:hover {
  background: rgba(255, 255, 255, 0.05);
}

.track-item.active {
  background: rgba(239, 68, 68, 0.12);
  border: 1px solid rgba(239, 68, 68, 0.35);
}

.col-num {
  font-size: 0.85rem;
  color: var(--text-dim);
  font-weight: 600;
  display: flex;
  align-items: center;
}

.track-playing-icon {
  display: flex;
  gap: 2px;
  align-items: flex-end;
}

.track-info-cell {
  display: flex;
  align-items: center;
  gap: 12px;
  min-width: 0;
  overflow: hidden;
}

.track-info-cell > div {
  min-width: 0;
  flex: 1;
  overflow: hidden;
}

@media (max-width: 640px) {
  .track-info-cell {
    gap: 8px;
  }
}

.track-thumb {
  width: 44px;
  height: 44px;
  min-width: 44px;
  border-radius: var(--radius-sm);
  object-fit: cover;
  flex-shrink: 0;
}

@media (max-width: 640px) {
  .track-thumb {
    width: 38px;
    height: 38px;
    min-width: 38px;
  }
}

@media (max-width: 380px) {
  .track-thumb {
    width: 32px;
    height: 32px;
    min-width: 32px;
  }
}

.track-name {
  font-size: 0.95rem;
  color: #fff;
  margin-bottom: 2px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: block;
}

@media (max-width: 640px) {
  .track-name {
    font-size: 0.88rem;
  }
}

.track-item.active .track-name {
  color: var(--accent-red-bright);
}

.track-artist-sub {
  font-size: 0.78rem;
  color: var(--text-dim);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: block;
}

.track-duration-cell {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  font-size: 0.85rem;
  color: var(--text-dim);
  font-variant-numeric: tabular-nums;
  font-weight: 600;
}

@media (max-width: 640px) {
  .track-duration-cell {
    font-size: 0.78rem;
  }
}

.hub-icon-img {
  width: 18px;
  height: 18px;
  object-fit: contain;
  display: inline-block;
  flex-shrink: 0;
}

.streaming-hub-banner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-md);
  padding: 16px 20px;
  margin-top: 24px;
  gap: 14px;
  width: 100%;
  box-sizing: border-box;
}

.hub-text {
  min-width: 0;
}

.hub-text strong {
  display: block;
  font-size: 0.92rem;
  color: #fff;
}

.hub-text span {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.hub-buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  align-items: center;
}

.btn-sm {
  padding: 8px 16px;
  font-size: 0.82rem;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

@media (max-width: 768px) {
  .streaming-hub-banner {
    flex-direction: column;
    text-align: center;
    padding: 16px 12px;
    gap: 14px;
  }

  .hub-text {
    text-align: center;
    width: 100%;
  }

  .hub-buttons {
    width: 100%;
    justify-content: center;
    gap: 8px;
  }

  .btn-sm {
    flex: 1 1 calc(33.333% - 8px);
    min-width: 95px;
    padding: 9px 10px;
    font-size: 0.8rem;
    justify-content: center;
  }
}

@media (max-width: 440px) {
  .hub-buttons {
    display: grid;
    grid-template-columns: 1fr;
    width: 100%;
    gap: 8px;
  }

  .btn-sm {
    width: 100%;
    padding: 10px 14px;
    font-size: 0.85rem;
  }
}
</style>
