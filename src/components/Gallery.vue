<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface GalleryItem {
  id: number
  title: string
  src: string
  year: string
}

// Ordered for visual diversity and high aesthetic impact
const items: GalleryItem[] = [
  {
    id: 1,
    title: 'Noche en la Ciudad',
    src: '/images/galery/627501371_18217120414314191_5529003263618785762_n.jpg',
    year: '2025'
  },
  {
    id: 2,
    title: 'Sesión de Estudio',
    src: '/images/galery/622285739_18089837225022815_812844266199420628_n.webp',
    year: '2024'
  },
  {
    id: 3,
    title: 'Trap Attitude',
    src: '/images/galery/638928428_18560244745060412_875903933980467593_n.jpg',
    year: '2020'
  },
  {
    id: 4,
    title: 'En la Cabina',
    src: '/images/galery/622793186_18105818464703427_6075701612837624420_n.webp',
    year: '2022'
  },
  {
    id: 5,
    title: 'Flow Urbano',
    src: '/images/galery/654479758_18097724968806873_6691550208992154810_n.webp',
    year: '2023'
  },
  {
    id: 6,
    title: 'Vive Nuestra Música',
    src: '/images/galery/621564256_18067374056196918_7790589735866060271_n.webp',
    year: '2023'
  }
]

const activeModalIndex = ref<number | null>(null)

const openLightbox = (index: number) => {
  activeModalIndex.value = index
  document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
  activeModalIndex.value = null
  document.body.style.overflow = 'auto'
}

const nextImage = () => {
  if (activeModalIndex.value === null) return
  activeModalIndex.value = (activeModalIndex.value + 1) % items.length
}

const prevImage = () => {
  if (activeModalIndex.value === null) return
  activeModalIndex.value = (activeModalIndex.value - 1 + items.length) % items.length
}

const handleKeydown = (e: KeyboardEvent) => {
  if (activeModalIndex.value === null) return
  if (e.key === 'Escape') closeLightbox()
  if (e.key === 'ArrowRight') nextImage()
  if (e.key === 'ArrowLeft') prevImage()
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = 'auto'
})
</script>

<template>
  <section id="galeria" class="gallery-section section-padding">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">GALERÍA <span class="gradient-text-red">VISUAL</span></h2>
        <p class="section-desc">
          Sesiones fotográficas, presentaciones y momentos destacados de DeepLower.
        </p>
      </div>

      <!-- Gallery Grid -->
      <div class="gallery-grid">
        <div 
          v-for="(item, index) in items" 
          :key="item.id" 
          class="gallery-card"
          @click="openLightbox(index)"
        >
          <div class="card-media">
            <img :src="item.src" :alt="item.title" class="gallery-img" loading="lazy" />
            <div class="card-overlay">
              <span class="view-icon">🔍</span>
              <div class="card-meta">
                <h3 class="card-title">{{ item.title }}</h3>
                <span class="card-year">{{ item.year }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Lightbox Modal -->
    <div 
      v-if="activeModalIndex !== null" 
      class="lightbox-modal"
      @click.self="closeLightbox"
    >
      <button class="modal-close-btn" @click="closeLightbox" aria-label="Cerrar ventana">
        ✕
      </button>

      <button class="modal-nav-btn prev-btn" @click="prevImage" aria-label="Foto anterior">
        ❮
      </button>

      <div class="modal-content">
        <img 
          :src="items[activeModalIndex].src" 
          :alt="items[activeModalIndex].title" 
          class="modal-img"
        />
        <div class="modal-caption-box">
          <div class="modal-header-row">
            <span class="modal-year">{{ items[activeModalIndex].year }}</span>
            <span class="modal-counter">{{ activeModalIndex + 1 }} / {{ items.length }}</span>
          </div>
          <h4 class="modal-title">{{ items[activeModalIndex].title }}</h4>
        </div>
      </div>

      <button class="modal-nav-btn next-btn" @click="nextImage" aria-label="Foto siguiente">
        ❯
      </button>
    </div>
  </section>
</template>

<style scoped>
.gallery-section {
  position: relative;
}

/* Gallery Grid */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  margin-top: 40px;
}

@media (max-width: 992px) {
  .gallery-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 18px;
  }
}

@media (max-width: 580px) {
  .gallery-grid {
    grid-template-columns: 1fr;
  }
}

.gallery-card {
  border-radius: var(--radius-lg);
  overflow: hidden;
  cursor: pointer;
  background: var(--bg-surface);
  border: 1px solid var(--border-subtle);
  transition: all var(--transition-smooth);
}

.gallery-card:hover {
  transform: translateY(-6px);
  border-color: rgba(239, 68, 68, 0.4);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.7), 0 0 20px rgba(239, 68, 68, 0.2);
}

.card-media {
  position: relative;
  aspect-ratio: 4/5;
  overflow: hidden;
}

.gallery-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.gallery-card:hover .gallery-img {
  transform: scale(1.06);
}

.card-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.92) 0%, rgba(0, 0, 0, 0.2) 50%, transparent 100%);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 22px;
  opacity: 0.95;
  transition: opacity var(--transition-fast);
}

.view-icon {
  align-self: flex-end;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(8px);
  padding: 8px;
  border-radius: 50%;
  font-size: 0.9rem;
  border: 1px solid var(--border-subtle);
  transition: transform var(--transition-fast);
}

.gallery-card:hover .view-icon {
  transform: scale(1.15) rotate(10deg);
  background: var(--accent-red);
}

.card-meta {
  display: flex;
  flex-direction: column;
}

.card-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 4px;
}

.card-year {
  font-size: 0.8rem;
  color: var(--accent-red-bright);
  font-weight: 700;
  letter-spacing: 0.06em;
}

/* Lightbox Modal */
.lightbox-modal {
  position: fixed;
  inset: 0;
  z-index: 2000;
  background: rgba(0, 0, 0, 0.96);
  backdrop-filter: blur(20px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  animation: fadeIn 0.25s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal-content {
  position: relative;
  max-width: 820px;
  width: 100%;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
  border-radius: var(--radius-lg);
  overflow: hidden;
  background: rgba(14, 14, 18, 0.9);
  border: 1px solid rgba(239, 68, 68, 0.3);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.95);
}

.modal-img {
  width: 100%;
  max-height: 68vh;
  object-fit: contain;
  background: #000;
}

.modal-caption-box {
  padding: 18px 24px;
  background: #0c0c0e;
}

.modal-header-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 6px;
}

.modal-year {
  font-size: 0.8rem;
  font-weight: 700;
  color: var(--accent-red);
  letter-spacing: 0.05em;
}

.modal-counter {
  font-size: 0.8rem;
  color: var(--text-dim);
}

.modal-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: #fff;
  margin: 0;
}

.modal-close-btn {
  position: absolute;
  top: 24px;
  right: 28px;
  font-size: 1.6rem;
  color: #fff;
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid var(--border-subtle);
  width: 44px;
  height: 44px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all var(--transition-fast);
  z-index: 10;
}

.modal-close-btn:hover {
  background: var(--accent-red);
  transform: rotate(90deg);
}

.modal-nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid var(--border-subtle);
  color: #fff;
  width: 52px;
  height: 52px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.4rem;
  cursor: pointer;
  transition: all var(--transition-fast);
  z-index: 10;
}

.modal-nav-btn:hover {
  background: var(--accent-red);
  transform: translateY(-50%) scale(1.1);
}

.prev-btn {
  left: 28px;
}

.next-btn {
  right: 28px;
}

@media (max-width: 768px) {
  .modal-nav-btn {
    width: 40px;
    height: 40px;
    font-size: 1.1rem;
  }
  .prev-btn { left: 10px; }
  .next-btn { right: 10px; }
}
</style>
