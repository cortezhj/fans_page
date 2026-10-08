<script setup lang="ts">
const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const currentYear = new Date().getFullYear()
</script>

<template>
  <footer class="footer">
    <div class="container footer-container">
      <div class="footer-top">
        <!-- Brand Info -->
        <div class="footer-brand">
          <a href="#inicio" class="footer-logo">
            <span class="logo-text">DEEP<span class="logo-highlight">LOWER</span></span>
          </a>
          <p class="footer-tagline">
            Sitio oficial de DeepLower. Música desde el alma para el mundo entero.
          </p>
        </div>

        <!-- Quick Links -->
        <div class="footer-links-col">
          <h4 class="footer-heading">Navegación</h4>
          <ul class="footer-nav">
            <li><a href="#inicio">Inicio</a></li>
            <li><a href="#bio">Sobre Mí</a></li>
            <li><a href="#musica">Música & Éxitos</a></li>
            <li><a href="#galeria">Galería de Fotos</a></li>
            <li><a href="#redes">Redes Sociales</a></li>
            <li><a href="#contacto">Booking</a></li>
          </ul>
        </div>

        <!-- Streaming Platforms -->
        <div class="footer-links-col">
          <h4 class="footer-heading">Plataformas</h4>
          <ul class="footer-nav">
            <li><a href="https://open.spotify.com/intl-es/artist/6PEn0Prb9VcwQq7tvlFYr7?si=RmIZcVxeQPW7EF7umwiBtw" target="_blank" rel="noopener noreferrer">Spotify</a></li>
            <li><a href="https://www.youtube.com/@Deep_Lower/featured" target="_blank" rel="noopener noreferrer">YouTube</a></li>
            <li><a href="https://soundcloud.com/deep-lower" target="_blank" rel="noopener noreferrer">SoundCloud</a></li>
          </ul>
        </div>

        <!-- Back to Top -->
        <div class="footer-back-col">
          <button class="back-to-top-btn" @click="scrollToTop" title="Volver al inicio">
            <span class="arrow-up">↑</span>
          </button>
        </div>
      </div>

      <div class="footer-bottom">
        <p class="copyright">
          © {{ currentYear }} <strong>DeepLower</strong>. Todos los derechos reservados.
        </p>
        <div class="legal-links">
          <span>Términos & Condiciones</span>
          <span>•</span>
          <span>Política de Privacidad</span>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: #050608;
  border-top: 1px solid var(--border-subtle);
  padding: 80px 0 36px;
  position: relative;
}

.footer-top {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 40px;
  margin-bottom: 60px;
}

@media (max-width: 900px) {
  .footer-top {
    grid-template-columns: 1fr 1fr;
    gap: 30px;
  }
}

@media (max-width: 580px) {
  .footer-top {
    grid-template-columns: 1fr;
  }
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 800;
  color: #fff;
  margin-bottom: 14px;
}

.logo-symbol {
  font-size: 1.3rem;
  filter: drop-shadow(0 0 10px var(--accent-red));
}

.logo-highlight {
  color: var(--accent-red);
}

.footer-tagline {
  color: var(--text-muted);
  font-size: 0.9rem;
  line-height: 1.6;
  max-width: 320px;
  margin-bottom: 18px;
}

.footer-tagline strong {
  color: #fff;
}

.footer-badge span {
  display: inline-block;
  padding: 4px 12px;
  background: rgba(239, 68, 68, 0.1);
  border: 1px solid rgba(239, 68, 68, 0.35);
  border-radius: var(--radius-full);
  color: var(--accent-red);
  font-size: 0.78rem;
  font-weight: 700;
}

.footer-heading {
  font-size: 0.95rem;
  color: #fff;
  margin-bottom: 18px;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.footer-nav {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.footer-nav a {
  color: var(--text-muted);
  font-size: 0.88rem;
  transition: all var(--transition-fast);
}

.footer-nav a:hover {
  color: var(--accent-red);
  padding-left: 4px;
}

.footer-back-col {
  display: flex;
  align-items: flex-start;
  justify-content: flex-end;
}

@media (max-width: 900px) {
  .footer-back-col {
    justify-content: flex-start;
  }
}

.back-to-top-btn {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 18px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-full);
  color: var(--text-muted);
  font-size: 0.85rem;
  font-weight: 700;
  transition: all var(--transition-fast);
}

.back-to-top-btn:hover {
  background: var(--accent-red);
  color: #fff;
  box-shadow: 0 0 16px var(--accent-red-glow);
  transform: translateY(-3px);
}

.arrow-up {
  font-size: 1.1rem;
}

.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 28px;
  border-top: 1px solid var(--border-subtle);
  font-size: 0.82rem;
  color: var(--text-dim);
  flex-wrap: wrap;
  gap: 14px;
}

.copyright strong {
  color: #fff;
}

.legal-links {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>
