<template>
  <div class="app">

    <!-- ──────────── HERO ──────────── -->
    <section class="hero">
      <div class="container">
        <div class="hero-grid">

          <div class="hero-text">
            <h1 class="hero-name">Daniel Roque.</h1>
            <p class="hero-desc">
              Estudiante de Ingeniería en Sistemas Computacionales en el Tecnológico de Morelia. 
              Desarrollador full stack y móvil enfocado en crear soluciones de software sólidas y escalables: 
              desde arquitecturas backend con FastAPI, Redis y bases de datos relacionales, 
              hasta aplicaciones móviles en React Native e interfaces web dinámicas integradas con modelos de IA.
            </p>
            
            <div class="hero-contacts">
              <a href="https://github.com/ImRoque" target="_blank" rel="noopener" class="contact-btn contact-btn--github" aria-label="GitHub">
                <img :src="github" class="btn-icon inv" alt="" />
                <span>GitHub</span>
              </a>
              <a href="https://www.instagram.com/roque.crts/" target="_blank" rel="noopener" class="contact-btn contact-btn--instagram" aria-label="Instagram">
                <img :src="instagram" class="btn-icon inv" alt="" />
                <span>Instagram</span>
              </a>
              <a href="https://wa.me/524439241432" target="_blank" rel="noopener" class="contact-btn contact-btn--whatsapp" aria-label="WhatsApp">
                <img :src="whatsappNegro" class="btn-icon inv" alt="" />
                <span>WhatsApp</span>
              </a>
              <a href="https://mail.google.com/mail/?view=cm&fs=1&to=droque.cts@gmail.com" target="_blank" rel="noopener" class="contact-btn contact-btn--gmail" aria-label="Gmail">
                <img :src="gmail" class="btn-icon" alt="" />
                <span>Email</span>
              </a>
            </div>
          </div>

          <div class="hero-img-wrap">
            <img :src="fotoDAANRC" alt="Daniel Roque" class="hero-photo" />
          </div>

        </div>
      </div>
    </section>

    <!-- ──────────── PROYECTOS ──────────── -->
    <section class="section" id="proyectos">
      <div class="container">
        <p class="eyebrow">/ 01 — Proyectos</p>
        <h2 class="section-heading">Cosas que he construido</h2>

        <div class="projects-grid">
          <component
            v-for="p in proyectos"
            :key="p.name"
            :is="p.link ? 'a' : 'article'"
            :href="p.link || undefined"
            :target="p.link ? '_blank' : undefined"
            :rel="p.link ? 'noopener' : undefined"
            class="proj-card"
          >
            <div class="proj-top">
              <div class="proj-logo-box">
                <img :src="p.logo" :alt="p.name" class="proj-logo" />
              </div>
              <span class="proj-link-icon" v-if="p.link">↗</span>
            </div>
            <div class="proj-body">
              <h3 class="proj-title">{{ p.name }}</h3>
              <p class="proj-desc">{{ p.desc }}</p>
            </div>
            <div class="proj-footer">
              <span v-for="t in p.stack" :key="t" class="proj-chip">{{ t }}</span>
            </div>
          </component>
        </div>
      </div>
    </section>

    <!-- ──────────── STACK (INTERACTIVO CON TABS) ──────────── -->
    <section class="section" id="stack">
      <div class="container">
        <div class="stack-header">
          <div>
            <p class="eyebrow">/ 02 — Stack</p>
            <h2 class="section-heading">Tecnologías que domino</h2>
          </div>

          <!-- Filtros interactivos -->
          <div class="stack-tabs" role="tablist">
            <button
              v-for="tab in tabs"
              :key="tab.id"
              :class="['stack-tab-btn', { active: activeTab === tab.id }]"
              @click="activeTab = tab.id"
              role="tab"
              :aria-selected="activeTab === tab.id"
            >
              {{ tab.label }}
            </button>
          </div>
        </div>

        <!-- Matriz interactiva de tecnologías con animación fluida y escalonada -->
        <Transition name="grid-swap" mode="out-in">
          <div :key="activeTab" class="tech-matrix">
            <div
              v-for="(t, idx) in filteredTecnologias"
              :key="t.name"
              class="tech-card"
              :style="{ '--delay': getCardDelay(idx) }"
            >
              <div class="tech-card-inner">
                <div class="tech-logo-wrap">
                  <img :src="t.logo" :alt="t.name" class="tech-card-logo" />
                </div>
                <div class="tech-card-meta">
                  <span class="tech-card-name">{{ t.name }}</span>
                  <span class="tech-card-type">{{ t.type }}</span>
                </div>
              </div>
            </div>
          </div>
        </Transition>

      </div>
    </section>

    <!-- ──────────── CONTACTO / CTA ──────────── -->
    <section class="section section--cta" id="contacto">
      <div class="container">
        <p class="eyebrow">/ 03 — Contacto</p>
        
        <div class="cta-box">
          <div class="cta-inner">
            <h2 class="cta-title">¿Tienes una idea en mente?</h2>
            <p class="cta-desc">
              Estoy disponible para colaborar en el desarrollo de aplicaciones web a medida,
              apps móviles para Android e iOS o la arquitectura de backend y APIs escalables.
              Si buscas materializar un proyecto o necesitas un desarrollador con iniciativa, 
              hablemos directamente.
            </p>

            <div class="cta-actions">
              <a 
                href="https://wa.me/524439241432" 
                target="_blank" 
                rel="noopener" 
                class="cta-btn cta-btn--whatsapp"
              >
                <img :src="whatsappNegro" class="cta-icon inv" alt="" />
                <span>Escríbeme por WhatsApp</span>
              </a>
              <a 
                href="https://mail.google.com/mail/?view=cm&fs=1&to=droque.cts@gmail.com" 
                target="_blank" 
                rel="noopener" 
                class="cta-btn cta-btn--gmail"
              >
                <img :src="gmail" class="cta-icon" alt="" />
                <span>Enviar correo directo</span>
              </a>
            </div>
          </div>
        </div>

      </div>
    </section>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import fotoDAANRC   from './images/fotoDAANRC.jpg';
import github       from './images/github.svg';
import instagram    from './images/instagram.svg';
import whatsappNegro from './images/whatsappNegro.svg';
import whatsapp     from './images/whatsapp.svg';
import gmail        from './images/gmail.svg';
import tailwindcss  from './images/tailwindcss.svg';
import react        from './images/react.svg';
import nodejs       from './images/nodejs.svg';
import js           from './images/js.svg';
import ts           from './images/ts.svg';
import python       from './images/python.svg';
import html5        from './images/html5.svg';
import css3         from './images/css3.svg';
import java         from './images/java.svg';
import postgres     from './images/postgres.svg';
import csharp       from './images/csharp.svg';
import mongodb      from './images/mongodb.svg';
import logoBloom    from './images/LogoBloomBeauty.png';
import logoCoffee   from './images/LogoCooffeeShop-App.png';
import logoTripTalk from './images/LogoTripTalk.png';
import logoDIF      from './images/DIF.jpg';

const activeTab = ref('all');

const tabs = [
  { id: 'all',      label: 'Todos' },
  { id: 'frontend', label: 'Frontend & Mobile' },
  { id: 'backend',  label: 'Backend & APIs' },
  { id: 'database', label: 'Bases de Datos' },
];

const proyectos = [
  {
    name: 'Bloom Beauty',
    logo: logoBloom,
    link: 'https://github.com/ImRoque/Bloom-Beauty',
    stack: ['React 19', 'Node.js', 'OpenAI'],
    desc:  'E-commerce de skincare con asistente IA integrado vía ChatGPT. Desarrollado full-stack con arquitectura modular y manejo seguro de variables de entorno.'
  },
  {
    name: 'CoffeeShop App',
    logo: logoCoffee,
    link: 'https://github.com/ArmandoCasanova/coffeeshop-app',
    stack: ['React Native', 'FastAPI', 'Redis', 'Stripe'],
    desc:  'Aplicación móvil transaccional con autenticación JWT, caché en memoria con Redis, procesamiento de pagos con Stripe y pruebas E2E automatizadas con Maestro.'
  },
  {
    name: 'TripTalk',
    logo: logoTripTalk,
    link: 'https://github.com/ImRoque/TripTalk',
    stack: ['Java', 'Android', 'C#', 'MySQL'],
    desc:  'Red social móvil orientada a viajeros para compartir rutas, experiencias y recomendaciones en comunidad, desarrollada con cliente nativo Android y backend relacional.'
  },
  {
    name: 'Lens Menu',
    logo: logoDIF,
    link: null,
    stack: ['OCR', 'LLM', 'WCAG 2.1'],
    desc:  'Protocolo de investigación junto a DIF Morelia: app de asistencia visual accesible que convierte menús analógicos a audio estructurado mediante visión computacional.'
  },
];

const tecnologias = [
  { name: 'JavaScript',   logo: js, category: 'frontend', type: 'Lenguaje' },
  { name: 'TypeScript',   logo: ts, category: 'frontend', type: 'Tipado estático' },
  { name: 'React Native', logo: react, category: 'frontend', type: 'Mobile Framework' },
  { name: 'HTML5',        logo: html5, category: 'frontend', type: 'Estructura web' },
  { name: 'CSS3',         logo: css3, category: 'frontend', type: 'Estilos web' },
  { name: 'TailwindCSS',  logo: tailwindcss, category: 'frontend', type: 'CSS Framework' },
  { name: 'Python',       logo: python, category: 'backend', type: 'Lenguaje / IA' },
  { name: 'FastAPI',      logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/fastapi/fastapi-original.svg', category: 'backend', type: 'Web Framework' },
  { name: 'Node.js',      logo: nodejs, category: 'backend', type: 'Runtime JavaScript' },
  { name: 'Java',         logo: java, category: 'backend', type: 'Lenguaje / Android' },
  { name: 'C#',           logo: csharp, category: 'backend', type: 'Lenguaje / Backend' },
  { name: 'PostgreSQL',   logo: postgres, category: 'database', type: 'SQL Relacional' },
  { name: 'MongoDB',      logo: mongodb, category: 'database', type: 'NoSQL Documental' },
];

const filteredTecnologias = computed(() => {
  if (activeTab.value === 'all') return tecnologias;
  return tecnologias.filter(t => t.category === activeTab.value);
});

const getCardDelay = (idx) => {
  // Cascada ágil y continua sin pausas perceptibles
  if (activeTab.value === 'all') {
    return `${idx * 35}ms`;
  }
  return `${idx * 45}ms`;
};
</script>

<style>
/* ═══════════════════════════════════════════
   FUENTE
═══════════════════════════════════════════ */
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,700;1,9..40,300&family=DM+Mono:wght@400;500&display=swap');

/* ═══════════════════════════════════════════
   VARIABLES
═══════════════════════════════════════════ */
:root {
  --bg:       #111111;
  --surface:  #181818;
  --surface-hover: #222222;
  --border:   #282828;
  --border-strong: #383838;
  --white:    #ffffff;
  --muted:    #8e8e8e;
  --radius:   16px;
  --max:      1120px;
}

/* ═══════════════════════════════════════════
   RESET
═══════════════════════════════════════════ */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body {
  background: var(--bg);
  color: var(--white);
  font-family: 'DM Sans', system-ui, sans-serif;
  -webkit-font-smoothing: antialiased;
  overflow-x: hidden;
}
a { text-decoration: none; color: inherit; }
ul { list-style: none; }
img { display: block; }
button { font-family: inherit; }

/* ═══════════════════════════════════════════
   CONTENEDOR
═══════════════════════════════════════════ */
.container {
  max-width: var(--max);
  margin: 0 auto;
  padding: 0 clamp(20px, 6vw, 64px);
}

/* ═══════════════════════════════════════════
   HERO
═══════════════════════════════════════════ */
.hero {
  padding: clamp(70px, 12vw, 120px) 0 clamp(60px, 10vw, 90px);
  border-bottom: 1px solid var(--border);
}

.hero-grid {
  display: grid;
  grid-template-columns: 1.15fr 0.85fr;
  gap: clamp(32px, 5vw, 64px);
  align-items: center;
}

/* Nombre con tamaño controlado y equilibrado */
.hero-name {
  font-size: clamp(2.4rem, 5.5vw, 4.2rem);
  font-weight: 700;
  line-height: 1.05;
  letter-spacing: -0.04em;
  color: var(--white);
  margin-bottom: 24px;
}

.hero-desc {
  font-size: clamp(1rem, 1.4vw, 1.12rem);
  line-height: 1.7;
  color: var(--muted);
  max-width: 580px;
  margin-bottom: 36px;
  font-weight: 300;
}

/* Modos de contacto destacados */
.hero-contacts {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.contact-btn {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: var(--surface);
  border: 1px solid var(--border);
  padding: 10px 18px;
  border-radius: 999px;
  font-size: 0.88rem;
  font-weight: 500;
  color: var(--white);
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

/* Todos los paneles comparten exactamente el mismo fondo y borde por defecto */
.contact-btn--github,
.contact-btn--instagram,
.contact-btn--whatsapp,
.contact-btn--gmail {
  background: var(--surface);
  border: 1px solid var(--border);
}

/* Hover GitHub: Gris */
.contact-btn--github:hover {
  background: var(--surface-hover);
  border-color: #8b949e;
  box-shadow: 0 4px 20px rgba(255, 255, 255, 0.12);
  transform: translateY(-2px);
}

/* Hover Instagram: Morado-rosa degradado oficial */
.contact-btn--instagram:hover {
  background: linear-gradient(var(--surface-hover), var(--surface-hover)) padding-box,
              linear-gradient(135deg, #833ab4 0%, #fd1d1d 50%, #fcb045 100%) border-box;
  border: 1px solid transparent;
  box-shadow: 0 4px 22px rgba(225, 48, 108, 0.38), 0 0 12px rgba(131, 58, 180, 0.25);
  transform: translateY(-2px);
}

/* Hover WhatsApp: Verde característico #25D366 */
.contact-btn--whatsapp:hover {
  background: var(--surface-hover);
  border-color: #25d366;
  box-shadow: 0 4px 22px rgba(37, 211, 102, 0.38);
  transform: translateY(-2px);
}

/* Hover Gmail: Arcoíris Google con difuminación cromática */
.contact-btn--gmail:hover {
  background: linear-gradient(var(--surface-hover), var(--surface-hover)) padding-box,
              linear-gradient(135deg, #4285f4 0%, #ea4335 33%, #fbbc05 66%, #34a853 100%) border-box;
  border: 1px solid transparent;
  box-shadow: 
    -4px 4px 20px -2px rgba(66, 133, 244, 0.4),   /* Azul Google */
    0px -3px 20px -2px rgba(234, 67, 53, 0.4),    /* Rojo Google */
    4px -2px 18px -2px rgba(251, 188, 5, 0.35),   /* Amarillo Google */
    4px 4px 20px -2px rgba(52, 168, 83, 0.4);     /* Verde Google */
  transform: translateY(-2px);
}

.btn-icon {
  width: 18px;
  height: 18px;
  object-fit: contain;
}
.inv { filter: brightness(0) invert(1); }

/* Foto grande, a color, cuadrada con esquinas redondas */
.hero-img-wrap {
  display: flex;
  justify-content: center;
  align-items: center;
}

.hero-photo {
  width: 100%;
  max-width: 350px;
  aspect-ratio: 1;
  border-radius: 32px;
  object-fit: cover;
  border: 1px solid var(--border-strong);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
  transition: transform 0.3s ease, border-color 0.3s ease;
}

.hero-photo:hover {
  transform: translateY(-4px) scale(1.01);
  border-color: rgba(255, 255, 255, 0.35);
}

/* ═══════════════════════════════════════════
   SECCIÓN BASE
═══════════════════════════════════════════ */
.section {
  padding: clamp(70px, 10vw, 110px) 0;
  border-bottom: 1px solid var(--border);
}

.eyebrow {
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem;
  color: var(--muted);
  letter-spacing: 0.05em;
  margin-bottom: 14px;
}

.section-heading {
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  margin-bottom: clamp(36px, 6vw, 60px);
}

/* ═══════════════════════════════════════════
   PROYECTOS
═══════════════════════════════════════════ */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 24px;
}

.proj-card {
  display: flex;
  flex-direction: column;
  gap: 20px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 28px;
  transition: border-color 0.25s, transform 0.25s;
  cursor: pointer;
}

.proj-card:hover {
  border-color: rgba(255, 255, 255, 0.3);
  transform: translateY(-4px);
}

.proj-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
}

.proj-logo-box {
  width: 58px;
  height: 58px;
  background: #ffffff;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px;
  border: 1px solid #e5e5e5;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.08);
}

.proj-logo {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

.proj-link-icon {
  font-size: 1.3rem;
  color: var(--muted);
  transition: color 0.2s, transform 0.2s;
  line-height: 1;
}

.proj-card:hover .proj-link-icon {
  color: var(--white);
  transform: translate(3px, -3px);
}

.proj-title {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 10px;
}

.proj-desc {
  font-size: 0.95rem;
  color: var(--muted);
  line-height: 1.6;
  font-weight: 300;
}

.proj-footer {
  margin-top: auto;
  padding-top: 20px;
  border-top: 1px solid var(--border);
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.proj-chip {
  font-family: 'DM Mono', monospace;
  font-size: 0.72rem;
  color: var(--muted);
  letter-spacing: 0.03em;
}

.proj-chip:not(:last-child)::after {
  content: ' ·';
}

/* ═══════════════════════════════════════════
   STACK INTERACTIVO (MATRIZ CON TABS)
═══════════════════════════════════════════ */
.stack-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-wrap: wrap;
  gap: 24px;
  margin-bottom: 36px;
}
.stack-header .section-heading {
  margin-bottom: 0;
}

.stack-tabs {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  background: var(--surface);
  border: 1px solid var(--border);
  padding: 6px;
  border-radius: 999px;
}

.stack-tab-btn {
  background: transparent;
  border: none;
  color: var(--muted);
  font-size: 0.85rem;
  font-weight: 500;
  padding: 8px 16px;
  border-radius: 999px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.stack-tab-btn:hover {
  color: var(--white);
}

.stack-tab-btn.active {
  background: var(--white);
  color: #000000;
  font-weight: 600;
}

.tech-matrix {
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
}

/* Transición de intercambio de pestañas para el contenedor */
.grid-swap-leave-active {
  transition: opacity 0.16s ease, transform 0.16s ease;
}

.grid-swap-leave-to {
  opacity: 0;
  transform: scale(0.98);
}

.grid-swap-enter-active {
  transition: opacity 0.15s ease;
}

.grid-swap-enter-from {
  opacity: 0;
}

/* Efecto Blur-to-Focus con Pop orgánico:
   - Se ejecuta directamente en cada .tech-card dentro de .tech-matrix (nunca se trunca prematuramente por el contenedor de Vue).
   - El desenfoque (blur) se disuelve de forma 100% gradual durante el ascenso:
     0%: 10px -> 45%: 3px -> 75%: 0px (el blur llega a cero exactamente en el punto de máxima velocidad del pop).
   - El pop escala de 0.92 a 1.025 (overshoot natural) y se asienta suavemente en 1.0.
   - font-smoothing antialiased y backface-visibility evitan cualquier parpadeo de ClearType o salto subpixel en Windows.
*/
.tech-matrix .tech-card {
  animation: cardBlurPop 0.48s cubic-bezier(0.2, 0.9, 0.3, 1) both;
  animation-delay: var(--delay, 0ms);
  will-change: opacity, transform, filter;
  transform-origin: center center;
  backface-visibility: hidden;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

@keyframes cardBlurPop {
  0% {
    opacity: 0;
    filter: blur(8px);
    transform: translate3d(0, 16px, 0) scale(0.93);
  }
  45% {
    opacity: 1;
    filter: blur(0px);
    transform: translate3d(0, -3px, 0) scale(1.025);
  }
  100% {
    opacity: 1;
    filter: blur(0px);
    transform: translate3d(0, 0, 0) scale(1);
  }
}

.tech-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px 18px;
  cursor: default;
  transition: transform 0.25s cubic-bezier(0.2, 0.9, 0.3, 1), 
              border-color 0.2s ease, 
              background 0.2s ease;
  backface-visibility: hidden;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.tech-card:hover {
  border-color: rgba(255, 255, 255, 0.35);
  background: var(--surface-hover);
  transform: translateY(-3px) scale(1);
}

.tech-card-inner {
  display: flex;
  align-items: center;
  gap: 14px;
}

.tech-logo-wrap {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  transition: transform 0.2s ease;
}

.tech-card:hover .tech-logo-wrap {
  transform: scale(1.08);
}

.tech-card-logo {
  width: 22px;
  height: 22px;
  object-fit: contain;
}

.tech-card-meta {
  display: flex;
  flex-direction: column;
  gap: 2px;
  min-width: 0;
}

.tech-card-name {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--white);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.tech-card-type {
  font-family: 'DM Mono', monospace;
  font-size: 0.7rem;
  color: var(--muted);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* ═══════════════════════════════════════════
   CONTACTO / CTA SECTION
═══════════════════════════════════════════ */
.section--cta {
  border-bottom: none;
  padding-bottom: clamp(80px, 14vw, 130px);
}

.cta-box {
  background: linear-gradient(135deg, rgba(35, 35, 35, 0.7), rgba(20, 20, 20, 0.9));
  border: 1px solid var(--border-strong);
  border-radius: 24px;
  padding: clamp(36px, 6vw, 64px);
  position: relative;
  overflow: hidden;
}

.cta-box::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
}

.cta-inner {
  max-width: 680px;
}

.cta-title {
  font-size: clamp(1.8rem, 4vw, 2.6rem);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.15;
  color: var(--white);
  margin-bottom: 20px;
}

.cta-desc {
  font-size: clamp(1rem, 1.3vw, 1.1rem);
  line-height: 1.7;
  color: var(--muted);
  margin-bottom: 36px;
  font-weight: 300;
}

.cta-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}

.cta-btn {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  padding: 14px 26px;
  border-radius: 999px;
  font-size: 0.95rem;
  font-weight: 600;
  background: var(--surface);
  border: 1px solid var(--border-strong);
  color: var(--white);
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

.cta-btn--whatsapp:hover {
  background: var(--surface-hover);
  border-color: #25d366;
  box-shadow: 0 4px 24px rgba(37, 211, 102, 0.38);
  transform: translateY(-2px);
}

.cta-btn--gmail:hover {
  background: linear-gradient(var(--surface-hover), var(--surface-hover)) padding-box,
              linear-gradient(135deg, #4285f4 0%, #ea4335 33%, #fbbc05 66%, #34a853 100%) border-box;
  border: 1px solid transparent;
  box-shadow: 
    -4px 4px 20px -2px rgba(66, 133, 244, 0.4),
    0px -3px 20px -2px rgba(234, 67, 53, 0.4),
    4px -2px 18px -2px rgba(251, 188, 5, 0.35),
    4px 4px 20px -2px rgba(52, 168, 83, 0.4);
  transform: translateY(-2px);
}

.cta-icon {
  width: 20px;
  height: 20px;
  object-fit: contain;
}

/* ═══════════════════════════════════════════
   RESPONSIVE
═══════════════════════════════════════════ */
@media (max-width: 860px) {
  .hero-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .hero-img-wrap {
    order: -1;
    justify-content: flex-start;
  }
  .hero-photo {
    max-width: 240px;
    border-radius: 24px;
  }
  .stack-header {
    flex-direction: column;
    align-items: flex-start;
  }
}

@media (max-width: 600px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  .tech-matrix {
    grid-template-columns: 1fr;
  }
  .cta-actions {
    flex-direction: column;
  }
  .cta-btn {
    width: 100%;
    justify-content: center;
  }
}

/* ═══════════════════════════════════════════
   REDUCED MOTION
═══════════════════════════════════════════ */
@media (prefers-reduced-motion: reduce) {
  * { transition-duration: 0.01ms !important; }
}
</style>