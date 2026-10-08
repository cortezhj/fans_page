<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'Inicio', href: '#inicio' },
  { name: 'Sobre Mí', href: '#bio' },
  { name: 'Música', href: '#musica' },
  { name: 'Galería', href: '#galeria' },
  { name: 'Comunidad', href: '#redes' },
  { name: 'Contacto', href: '#contacto' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 40
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header 
    class="navbar" 
    :class="{ 
      'navbar-scrolled': isScrolled,
      'navbar-mobile-open': isMobileMenuOpen 
    }"
  >
    <div class="container nav-container">
      <!-- Logo -->
      <a href="#inicio" class="nav-logo" @click="closeMobileMenu">
        <span class="logo-text">DEEP<span class="logo-highlight">LOWER</span></span>
      </a>

      <!-- Desktop Navigation Links -->
      <nav class="nav-menu">
        <a 
          v-for="link in navLinks" 
          :key="link.name" 
          :href="link.href" 
          class="nav-link"
        >
          {{ link.name }}
        </a>
      </nav>

      <!-- Action Button & Streaming Quick Access -->
      <div class="nav-actions">
        <a href="#musica" class="btn btn-red nav-cta">
          <span>▶ Escuchar Ahora</span>
        </a>
        <button 
          class="mobile-toggle" 
          @click="toggleMobileMenu" 
          :aria-expanded="isMobileMenuOpen"
          aria-label="Abrir menú"
        >
          <span class="bar" :class="{ 'open': isMobileMenuOpen }"></span>
          <span class="bar" :class="{ 'open': isMobileMenuOpen }"></span>
          <span class="bar" :class="{ 'open': isMobileMenuOpen }"></span>
        </button>
      </div>
    </div>

    <!-- Mobile Drawer -->
    <div class="mobile-drawer" :class="{ 'is-open': isMobileMenuOpen }">
      <nav class="mobile-nav">
        <a 
          v-for="link in navLinks" 
          :key="link.name" 
          :href="link.href" 
          class="mobile-nav-link"
          @click="closeMobileMenu"
        >
          {{ link.name }}
        </a>
        <a href="#musica" class="btn btn-red mobile-cta" @click="closeMobileMenu">
          ▶ Escuchar Éxitos
        </a>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  transition: all var(--transition-smooth);
  padding: 22px 0;
  background: transparent;
}

.navbar-scrolled,
.navbar-mobile-open {
  padding: 14px 0;
  background: rgba(0, 0, 0, 0.72);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);
}

.nav-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: var(--font-display);
  font-size: 1.45rem;
  font-weight: 800;
  letter-spacing: 0.05em;
  color: #fff;
  transition: transform var(--transition-fast);
}

.nav-logo:hover {
  transform: scale(1.03);
}

.logo-symbol {
  font-size: 1.3rem;
  filter: drop-shadow(0 0 10px var(--accent-red));
}

.logo-highlight {
  color: var(--accent-red);
  text-shadow: 0 0 16px var(--accent-red-glow);
}

.nav-menu {
  display: flex;
  align-items: center;
  gap: 28px;
}

@media (max-width: 992px) {
  .nav-menu {
    display: none;
  }
}

.nav-link {
  font-size: 0.92rem;
  font-weight: 600;
  color: var(--text-muted);
  transition: color var(--transition-fast);
  position: relative;
  padding: 6px 0;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--accent-red);
  box-shadow: 0 0 8px var(--accent-red);
  transition: width var(--transition-smooth);
  border-radius: 2px;
}

.nav-link:hover {
  color: #fff;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 16px;
}

.nav-cta {
  padding: 10px 22px;
  font-size: 0.88rem;
}

@media (max-width: 580px) {
  .nav-cta {
    display: none;
  }
}

/* Mobile Toggle Hamburger */
.mobile-toggle {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 6px;
  width: 42px;
  height: 42px;
  padding: 8px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-sm);
  cursor: pointer;
}

@media (max-width: 992px) {
  .mobile-toggle {
    display: flex;
  }
}

.bar {
  width: 100%;
  height: 2px;
  background-color: #fff;
  border-radius: 2px;
  transition: all var(--transition-fast);
}

.bar.open:nth-child(1) {
  transform: translateY(8px) rotate(45deg);
}
.bar.open:nth-child(2) {
  opacity: 0;
}
.bar.open:nth-child(3) {
  transform: translateY(-8px) rotate(-45deg);
}

/* Mobile Drawer */
.mobile-drawer {
  display: none;
  position: fixed;
  top: 70px;
  left: 0;
  width: 100%;
  background: rgba(0, 0, 0, 0.72);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  padding: 24px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
  transform: translateY(-120%);
  transition: transform var(--transition-smooth);
}

@media (max-width: 992px) {
  .mobile-drawer {
    display: block;
  }
}

.mobile-drawer.is-open {
  transform: translateY(0);
}

.mobile-nav {
  display: flex;
  flex-direction: column;
  gap: 16px;
  text-align: center;
}

.mobile-nav-link {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-muted);
  padding: 10px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.04);
}

.mobile-nav-link:hover {
  color: var(--accent-red);
}

.mobile-cta {
  margin-top: 12px;
  width: 100%;
}
</style>
