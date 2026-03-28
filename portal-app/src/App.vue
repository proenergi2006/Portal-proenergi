<template>
  <div class="portal-page" :class="{ 'theme-dark': isDark }">
    <transition name="fade">
      <div v-if="isLoading" class="loading-screen">
        <div class="loading-box">
          <div class="loading-logo">
            <img :src="logoProenergi" alt="Logo Proenergi" class="loading-logo-img" />
          </div>

          <h2>Proenergi Application Portal</h2>
          <p>Menyiapkan gateway aplikasi perusahaan...</p>

          <div class="loading-bar">
            <span></span>
          </div>
        </div>
      </div>
    </transition>

    <div
      class="bg-scene"
      :style="{ backgroundImage: `url(${bgPortalFinal})` }"
    ></div>

    <header class="topbar">
      <div class="brand-wrap fade-up delay-1">
        <div class="brand-logo image-logo">
          <img :src="logoProenergi" alt="Logo Proenergi" class="brand-logo-img" />
        </div>

        <div class="brand-text">
          <p class="eyebrow">Proenergi Corporate Portal</p>
          <h1>Application Gateway</h1>
          <small>Akses terpadu untuk sistem internal perusahaan</small>
        </div>
      </div>

      <div class="header-actions fade-up delay-2">
        <div class="status-chip">
          <span class="status-dot"></span>
          Internal Secure Network
        </div>

        <div class="clock-card">
          <span>Waktu Saat Ini</span>
          <strong>{{ currentTime }}</strong>
        </div>

        <button class="theme-toggle" @click="isDark = !isDark">
          {{ isDark ? '☀ Light' : '🌙 Soft Dark' }}
        </button>
      </div>
    </header>

    <main class="hero-layout">
      <section class="hero-panel fade-up delay-2">
        <div class="hero-glow"></div>

        <div class="hero-badge">
          <span class="pulse-dot"></span>
          Unified Enterprise Access
        </div>

        <h2>
          <span class="title-line">Halaman Portal Akses</span>
          <span class="title-line">
            <span class="fuel-text">Proenergi Fuel</span>,
            <span class="crs-text">CRS</span>, dan
            <span class="helpdesk-text">Helpdesk</span>
          </span>
        </h2>

        <p class="hero-desc">
          Akses terpusat untuk seluruh sistem internal perusahaan secara cepat,
          aman, dan profesional.
        </p>

        <div class="hero-actions">
          <button class="btn btn-fuel" @click="openApp(apps[0].url)">
            <span class="btn-shine"></span>
            <FuelIcon class="btn-icon" />
            Masuk Proenergi Fuel
          </button>

          <button class="btn btn-crs" @click="openApp(apps[1].url)">
            <span class="btn-shine"></span>
            <StoneIcon class="btn-icon" />
            Masuk CRS
          </button>

          <button class="btn btn-helpdesk" @click="openApp(apps[2].url)">
            <span class="btn-shine"></span>
            <HelpdeskIcon class="btn-icon" />
            Masuk Helpdesk
          </button>
        </div>

        <div class="hero-stats">
          <div class="stat-card">
            <div class="stat-icon">◆</div>
            <strong>3</strong>
            <span>Core Systems</span>
          </div>

          <div class="stat-card">
            <div class="stat-icon">●</div>
            <strong>24/7</strong>
            <span>Internal Access</span>
          </div>

          <div class="stat-card">
            <div class="stat-icon">✦</div>
            <strong>Secure</strong>
            <span>Enterprise Gateway</span>
          </div>
        </div>
      </section>
    </main>

    <footer class="footer fade-up delay-4">
      © 2026 Proenergi Application Portal • Internal Enterprise Access
    </footer>
  </div>
</template>

<script setup>
import { h, onMounted, onBeforeUnmount, ref } from 'vue'
import logoProenergi from '@/assets/logo_pe_new.png'
import bgPortalFinal from '@/assets/bg-portal.png'

const isLoading = ref(true)
const isDark = ref(false)
const currentTime = ref('')
let timer = null

const FuelIcon = {
  name: 'FuelIcon',
  render() {
    return h(
      'svg',
      {
        viewBox: '0 0 24 24',
        fill: 'none',
        xmlns: 'http://www.w3.org/2000/svg',
      },
      [
        h('path', {
          d: 'M7 4H14C15.1046 4 16 4.89543 16 6V20H5V6C5 4.89543 5.89543 4 7 4Z',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linejoin': 'round',
        }),
        h('path', {
          d: 'M8 8H13',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linecap': 'round',
        }),
        h('path', {
          d: 'M16 8L18.5 10.5V16C18.5 16.8284 19.1716 17.5 20 17.5C20.8284 17.5 21.5 16.8284 21.5 16V11.5',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linecap': 'round',
          'stroke-linejoin': 'round',
        }),
      ]
    )
  },
}

const StoneIcon = {
  name: 'StoneIcon',
  render() {
    return h(
      'svg',
      {
        viewBox: '0 0 24 24',
        fill: 'none',
        xmlns: 'http://www.w3.org/2000/svg',
      },
      [
        h('path', {
          d: 'M5 14L8 7L16 5L20 11L17 18L9 19L5 14Z',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linejoin': 'round',
        }),
        h('path', {
          d: 'M8 7L12 12L20 11',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linejoin': 'round',
        }),
        h('path', {
          d: 'M12 12L9 19',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linejoin': 'round',
        }),
      ]
    )
  },
}

const HelpdeskIcon = {
  name: 'HelpdeskIcon',
  render() {
    return h(
      'svg',
      {
        viewBox: '0 0 24 24',
        fill: 'none',
        xmlns: 'http://www.w3.org/2000/svg',
      },
      [
        h('path', {
          d: 'M12 4C7.58172 4 4 7.58172 4 12V13',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linecap': 'round',
        }),
        h('path', {
          d: 'M20 13V12C20 7.58172 16.4183 4 12 4',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linecap': 'round',
        }),
        h('rect', {
          x: '3',
          y: '12',
          width: '4',
          height: '6',
          rx: '2',
          stroke: 'currentColor',
          'stroke-width': '1.8',
        }),
        h('rect', {
          x: '17',
          y: '12',
          width: '4',
          height: '6',
          rx: '2',
          stroke: 'currentColor',
          'stroke-width': '1.8',
        }),
        h('path', {
          d: 'M9 19C9.5 20 10.8 20.5 12 20.5C13.2 20.5 14.5 20 15 19',
          stroke: 'currentColor',
          'stroke-width': '1.8',
          'stroke-linecap': 'round',
        }),
      ]
    )
  },
}

const apps = [
  {
    name: 'Proenergi Fuel',
    url: 'https://syop.proenergi.com/proEnergi/',
  },
  {
    name: 'CRS',
    url: 'https://syop-crs.tridayaselaras.com/build/login',
  },
  {
    name: 'Helpdesk',
    url: 'https://helpdesk.proenergi.com',
  },
]

const updateClock = () => {
  const now = new Date()
  currentTime.value = now.toLocaleString('id-ID', {
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
  })
}

const openApp = url => {
  window.location.href = url
}

onMounted(() => {
  updateClock()
  timer = setInterval(updateClock, 1000)

  setTimeout(() => {
    isLoading.value = false
  }, 1400)
})

onBeforeUnmount(() => {
  if (timer) clearInterval(timer)
})
</script>

<style scoped>
:global(*) {
  box-sizing: border-box;
}

:global(html) {
  scroll-behavior: smooth;
}

:global(body) {
  margin: 0;
  font-family: Inter, Arial, sans-serif;
  background: #f7fbff;
}

.portal-page {
  --bg-main: linear-gradient(135deg, #edf5ff 0%, #ffffff 45%, #f6fff7 100%);
  --text-main: #0f172a;
  --text-soft: #475569;
  --panel: rgba(255, 255, 255, 0.78);
  --panel-strong: rgba(255, 255, 255, 0.9);
  --border: rgba(255, 255, 255, 0.72);
  --shadow: 0 24px 60px rgba(15, 23, 42, 0.1);
  position: relative;
  min-height: 100vh;
  overflow: hidden;
  padding: 32px;
  color: var(--text-main);
  background: var(--bg-main);
  transition: all 0.3s ease;
}

.portal-page.theme-dark {
  --bg-main: linear-gradient(135deg, #0f172a 0%, #111827 50%, #0b1220 100%);
  --text-main: #e5eefb;
  --text-soft: #b8c4d6;
  --panel: rgba(15, 23, 42, 0.62);
  --panel-strong: rgba(15, 23, 42, 0.78);
  --border: rgba(255, 255, 255, 0.08);
  --shadow: 0 24px 60px rgba(0, 0, 0, 0.35);
}

/* loading */
.loading-screen {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: grid;
  place-items: center;
  background:
    radial-gradient(circle at top left, rgba(37, 99, 235, 0.12), transparent 28%),
    radial-gradient(circle at bottom right, rgba(34, 197, 94, 0.1), transparent 24%),
    linear-gradient(135deg, #edf5ff, #ffffff, #f3fff6);
}

.loading-box {
  width: min(520px, calc(100vw - 32px));
  padding: 38px 34px 30px;
  border-radius: 32px;
  text-align: center;
  background: rgba(255, 255, 255, 0.72);
  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
  box-shadow: 0 30px 70px rgba(15, 23, 42, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.55);
}

.loading-logo {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px;
  background: transparent;
  box-shadow: none;
  border-radius: 0;
  width: 220px;
  max-width: 100%;
  min-height: 72px;
  animation: pulseLogoSoft 1.8s ease-in-out infinite;
}

.loading-logo-img {
  display: block;
  width: 100%;
  max-width: 200px;
  height: auto;
  object-fit: contain;
}

.loading-box h2 {
  margin: 0 0 8px;
  font-size: 24px;
  color: #0f172a;
}

.loading-box p {
  margin: 0 0 18px;
  color: #64748b;
}

.loading-bar {
  width: 100%;
  height: 10px;
  border-radius: 999px;
  background: #e2e8f0;
  overflow: hidden;
}

.loading-bar span {
  display: block;
  width: 45%;
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(90deg, #2563eb, #f97316, #22c55e, #7c3aed);
  animation: loadingSlide 1.5s ease-in-out infinite;
}

/* background image */
.bg-scene {
  position: absolute;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  opacity: 0.46;
}

.bg-scene::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.28) 0%,
    rgba(255, 255, 255, 0.22) 30%,
    rgba(255, 255, 255, 0.3) 100%
  );
}

.portal-page.theme-dark .bg-scene {
  opacity: 0.28;
}

.portal-page.theme-dark .bg-scene::after {
  background: linear-gradient(
    180deg,
    rgba(15, 23, 42, 0.52) 0%,
    rgba(15, 23, 42, 0.4) 35%,
    rgba(15, 23, 42, 0.58) 100%
  );
}

/* topbar */
.topbar {
  position: relative;
  z-index: 2;
  display: flex;
  justify-content: space-between;
  gap: 20px;
  align-items: center;
  margin-bottom: 28px;
}

.brand-wrap {
  display: flex;
  gap: 22px;
  align-items: center;
}

.brand-logo {
  display: flex;
  align-items: center;
  justify-content: center;
  width: auto;
  height: auto;
  background: transparent;
  box-shadow: none;
  border-radius: 0;
  overflow: visible;
  flex-shrink: 0;
}

.brand-logo-img {
  display: block;
  width: 170px;
  height: auto;
  object-fit: contain;
}

.eyebrow {
  margin: 0 0 4px;
  font-size: 12px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: #64748b;
}

.theme-dark .eyebrow {
  color: #9fb0c9;
}

.brand-text h1 {
  margin: 0;
  font-size: 30px;
  line-height: 1.1;
}

.brand-text small {
  display: inline-block;
  margin-top: 4px;
  color: var(--text-soft);
}

.header-actions {
  display: flex;
  gap: 12px;
  align-items: center;
  flex-wrap: wrap;
}

.status-chip {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 14px;
  border-radius: 999px;
  background: rgba(236, 253, 245, 0.8);
  border: 1px solid rgba(34, 197, 94, 0.18);
  color: #166534;
  font-size: 13px;
  font-weight: 700;
  backdrop-filter: blur(10px);
}

.status-dot {
  width: 9px;
  height: 9px;
  background: #22c55e;
  border-radius: 50%;
  box-shadow: 0 0 0 6px rgba(34, 197, 94, 0.12);
  animation: pulseDot 1.8s infinite;
}

.clock-card,
.theme-toggle {
  border: 1px solid var(--border);
  background: var(--panel);
  backdrop-filter: blur(14px);
  box-shadow: var(--shadow);
}

.clock-card {
  display: flex;
  flex-direction: column;
  gap: 4px;
  min-width: 250px;
  padding: 12px 16px;
  border-radius: 18px;
}

.clock-card span {
  font-size: 12px;
  color: var(--text-soft);
}

.clock-card strong {
  font-size: 15px;
}

.theme-toggle {
  padding: 12px 14px;
  border-radius: 16px;
  color: var(--text-main);
  cursor: pointer;
}

/* layout */
.hero-layout {
  position: relative;
  z-index: 2;
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
  align-items: start;
}

/* hero */
.hero-panel {
  position: relative;
  overflow: hidden;
  padding: 30px 34px 26px;
  border-radius: 30px;
  width: 100%;
  text-align: center;
  background: var(--panel);
  border: 1px solid var(--border);
  backdrop-filter: blur(16px);
  box-shadow: var(--shadow);
}

.hero-glow {
  position: absolute;
  right: -60px;
  top: -40px;
  width: 220px;
  height: 220px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(59, 130, 246, 0.18), transparent 70%);
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 9px 14px;
  border-radius: 999px;
  background: rgba(239, 246, 255, 0.92);
  color: #1d4ed8;
  font-size: 13px;
  font-weight: 700;
  animation: floatBadge 4s ease-in-out infinite;
}

.pulse-dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background: #2563eb;
}

.hero-panel h2 {
  margin: 20px 0 12px;
  font-size: 46px;
  line-height: 1.08;
}

.title-line {
  display: block;
}

.hero-desc {
  max-width: 760px;
  margin: 0 auto;
  font-size: 16px;
  line-height: 1.8;
  color: var(--text-soft);
}

.fuel-text {
  color: #2563eb;
}

.crs-text {
  color: #16a34a;
}

.helpdesk-text {
  color: #7c3aed;
}

.hero-actions {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 18px;
  flex-wrap: wrap;
  margin-top: 24px;
}

.btn {
  position: relative;
  overflow: hidden;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  min-width: 240px;
  padding: 18px 28px;
  border-radius: 18px;
  font-size: 16px;
  font-weight: 800;
  letter-spacing: 0.3px;
  color: white;
  border: none;
  cursor: pointer;
  transition: all 0.25s ease;
}

.btn:hover {
  transform: translateY(-4px) scale(1.01);
}

.btn-fuel {
  background: linear-gradient(135deg, #2563eb, #f97316);
  box-shadow: 0 20px 34px rgba(37, 99, 235, 0.22);
}

.btn-crs {
  background: linear-gradient(135deg, #16a34a, #84cc16);
  box-shadow: 0 20px 34px rgba(22, 163, 74, 0.2);
}

.btn-helpdesk {
  background: linear-gradient(135deg, #7c3aed, #2563eb);
  box-shadow: 0 20px 34px rgba(124, 58, 237, 0.2);
}

.btn-icon {
  width: 20px;
  height: 20px;
}

.btn-shine {
  position: absolute;
  top: 0;
  left: -140%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    100deg,
    transparent 20%,
    rgba(255, 255, 255, 0.35) 50%,
    transparent 80%
  );
  transform: skewX(-20deg);
  animation: shineMove 3.8s infinite;
}

.hero-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-top: 30px;
}

.stat-card {
  padding: 22px 18px;
  border-radius: 22px;
  background: var(--panel-strong);
  border: 1px solid var(--border);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.35);
}

.stat-icon {
  margin-bottom: 8px;
  font-size: 14px;
  color: #64748b;
}

.stat-card strong {
  display: block;
  font-size: 30px;
  margin-bottom: 6px;
}

.stat-card span {
  font-size: 14px;
  color: var(--text-soft);
}

/* footer */
.footer {
  position: relative;
  z-index: 2;
  width: fit-content;
  margin: 26px auto 0;
  padding: 10px 16px;
  text-align: center;
  color: var(--text-soft);
  font-size: 14px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.48);
  backdrop-filter: blur(10px);
}

.portal-page.theme-dark .footer {
  background: rgba(15, 23, 42, 0.45);
}

/* transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.35s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-up {
  animation: fadeUp 0.8s ease both;
}

.delay-1 { animation-delay: 0.08s; }
.delay-2 { animation-delay: 0.18s; }
.delay-3 { animation-delay: 0.28s; }
.delay-4 { animation-delay: 0.38s; }
.delay-5 { animation-delay: 0.48s; }

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(26px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulseLogoSoft {
  0%, 100% {
    transform: translateY(0) scale(1);
    opacity: 0.96;
  }
  50% {
    transform: translateY(-2px) scale(1.02);
    opacity: 1;
  }
}

@keyframes loadingSlide {
  0% {
    transform: translateX(-120%);
  }
  100% {
    transform: translateX(320%);
  }
}

@keyframes pulseDot {
  0% {
    box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.35);
  }
  70% {
    box-shadow: 0 0 0 8px rgba(34, 197, 94, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(34, 197, 94, 0);
  }
}

@keyframes shineMove {
  0% {
    left: -140%;
  }
  100% {
    left: 140%;
  }
}

@keyframes floatBadge {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-4px);
  }
}

/* responsive */
@media (max-width: 1180px) {
  .hero-panel h2 {
    font-size: 40px;
  }

  .btn {
    min-width: 220px;
  }
}

@media (max-width: 900px) {
  .brand-wrap {
    align-items: flex-start;
  }

  .brand-logo-img {
    width: 140px;
  }

  .hero-panel h2 {
    font-size: 36px;
  }

  .hero-stats {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .portal-page {
    padding: 20px;
  }

  .topbar {
    flex-direction: column;
    align-items: flex-start;
  }

  .header-actions {
    width: 100%;
    flex-direction: column;
    align-items: stretch;
  }

  .clock-card {
    min-width: auto;
    width: 100%;
  }

  .theme-toggle {
    width: 100%;
  }

  .hero-panel {
    padding: 24px 20px;
  }

  .hero-panel h2 {
    font-size: 30px;
  }

  .hero-actions {
    flex-direction: column;
  }

  .btn {
    width: 100%;
    min-width: unset;
    justify-content: center;
  }

  .brand-text h1 {
    font-size: 24px;
  }

  .brand-logo-img {
    width: 120px;
  }

  .loading-logo {
    width: 180px;
  }

  .loading-logo-img {
    max-width: 170px;
  }
}
</style>