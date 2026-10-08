<script setup lang="ts"></script>

<template>
  <section id="bio" class="bio-section section-padding section-white-theme">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">CONOCE A <span class="gradient-text-fire">DEEPLOWER</span></h2>
        <p class="section-desc">
          Detrás de los sintetizadores y los versos contundentes está la historia de Alejandro.
        </p>
      </div>

      <div class="bio-grid">
        <!-- Visual Column -->
        <div class="bio-image-col">
          <div class="bio-image-wrapper">
            <img src="/images/bio.jpg" alt="Alejandro Urbina (DeepLower) en el estudio de grabación" class="bio-img" />
            <div class="bio-image-backdrop"></div>
            <div class="bio-badge">
              <span class="bio-badge-icon">🎧</span>
              <div class="bio-badge-info">
                <strong>En el Estudio</strong>
                <span>Creando nuevo material</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Content Column -->
        <div class="bio-content-col">
          <div class="bio-artist-name">
            <span class="real-name">ALEJANDRO</span>
            <h3 class="stage-name gradient-text-fire">DEEPLOWER</h3>
          </div>

          <div class="bio-quote">
            <span class="quote-mark">“</span>
            <p>
              La música es la forma más honesta de expresar lo que sentimos.
            </p>
          </div>

          <div class="bio-text">
            <p>
              Iniciando su camino en la música urbana desde grabaciones caseras y batallas de improvisación, construyó su nombre <strong>DeepLower</strong> con una premisa clara: 
              romper los obstaculos y expresar su música sin limites.
            </p>
            <p>
              Con un estilo musical propio DeepLower se ha ganado el respeto esperando que sus oyentes encuentran en sus temas una voz genuina y sin poses.
            </p>
          </div>

          <div class="bio-cta-row">
            
            <a href="#contacto" class="btn btn-dark">
              <span>Contactar</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.bio-section {
  position: relative;
  overflow: hidden;
  background-color: #ffffff;
  color: #09090b;
}

.bio-grid {
  display: grid;
  grid-template-columns: 1fr 1.15fr;
  gap: 56px;
  align-items: center;
}

@media (max-width: 992px) {
  .bio-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}

.bio-image-col {
  position: relative;
}

.bio-image-wrapper {
  position: relative;
  border-radius: var(--radius-lg);
}

.bio-img {
  width: 100%;
  border-radius: var(--radius-lg);
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.18);
  position: relative;
  z-index: 2;
  transition: transform var(--transition-smooth);
}

.bio-image-wrapper:hover .bio-img {
  transform: translateY(-4px) scale(1.01);
}

.bio-image-backdrop {
  position: absolute;
  top: 16px;
  left: -12px;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(239, 68, 68, 0.35), rgba(0, 0, 0, 0.15));
  border-radius: var(--radius-lg);
  filter: blur(20px);
  z-index: 1;
}

.bio-badge {
  position: absolute;
  bottom: -18px;
  right: 18px;
  z-index: 3;
  display: flex;
  align-items: center;
  gap: 12px;
  background: #000000;
  border: 1px solid var(--accent-red);
  padding: 12px 20px;
  border-radius: var(--radius-md);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
}

.bio-badge-icon {
  font-size: 1.5rem;
}

.bio-badge-info strong {
  display: block;
  font-size: 0.9rem;
  color: #fff;
}

.bio-badge-info span {
  font-size: 0.75rem;
  color: var(--accent-red);
  font-weight: 600;
}

.bio-artist-name {
  margin-bottom: 20px;
}

.real-name {
  font-size: 1rem;
  font-weight: 800;
  letter-spacing: 0.15em;
  color: #71717a;
  display: block;
  margin-bottom: 4px;
}

.aka {
  font-size: 0.85rem;
  color: var(--accent-red);
  margin-right: 8px;
  font-weight: 700;
}

.stage-name {
  display: inline;
  font-size: clamp(2rem, 3.5vw, 3rem);
}

.bio-quote {
  position: relative;
  background: #f8fafc;
  border-left: 4px solid var(--accent-red);
  padding: 18px 24px;
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
  margin-bottom: 24px;
  border-top: 1px solid #f1f5f9;
  border-right: 1px solid #f1f5f9;
  border-bottom: 1px solid #f1f5f9;
}

.quote-mark {
  position: absolute;
  top: -10px;
  right: 16px;
  font-family: var(--font-display);
  font-size: 3.5rem;
  line-height: 1;
  color: rgba(239, 68, 68, 0.2);
  pointer-events: none;
}

.bio-quote p {
  font-size: 1.05rem;
  font-style: italic;
  color: #18181b;
  position: relative;
  z-index: 2;
  font-weight: 500;
}

.bio-text {
  display: flex;
  flex-direction: column;
  gap: 14px;
  color: #3f3f46;
  font-size: 1rem;
  line-height: 1.7;
  margin-bottom: 30px;
}

.bio-text strong {
  color: #000000;
}

.bio-highlights {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  margin-bottom: 32px;
}

@media (max-width: 600px) {
  .bio-highlights {
    grid-template-columns: 1fr;
  }
}

.highlight-card {
  display: flex;
  gap: 12px;
  padding: 14px;
  background: #f4f4f6;
  border: 1px solid #e4e4e7;
  border-radius: var(--radius-md);
  transition: all var(--transition-fast);
}

.highlight-card:hover {
  background: #ffffff;
  border-color: var(--accent-red);
  box-shadow: 0 4px 14px rgba(239, 68, 68, 0.15);
  transform: translateY(-2px);
}

.highlight-icon {
  font-size: 1.4rem;
  line-height: 1;
}

.highlight-title {
  font-size: 0.9rem;
  color: #000000;
  margin-bottom: 2px;
  font-weight: 700;
}

.highlight-desc {
  font-size: 0.8rem;
  color: #52525b;
  line-height: 1.35;
}

.bio-cta-row {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

@media (max-width: 580px) {
  .bio-badge {
    position: static;
    margin-top: 14px;
    width: 100%;
    box-sizing: border-box;
  }
  .bio-cta-row a {
    width: 100%;
    text-align: center;
    justify-content: center;
  }
}
</style>
