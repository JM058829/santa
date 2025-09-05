<template>
  <div id="top" class="page">
    <header class="site-header">
      <a href="#top" class="brand">
        <span class="brand-small">EL DE LA</span>
        <span class="brand-big">SANTA</span>
      </a>
      <nav class="nav">
        <a href="#media">Media</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
      </nav>
    </header>

    <section class="hero" @mousemove="onMove">
      <video
        v-if="hasVideo"
        class="hero-video"
        :src="videoUrl"
        autoplay
        muted
        loop
        playsinline
      ></video>
      <img v-else class="hero-bg" :src="bgUrl" alt="Background" />

      <!-- subtle animated smoke / glow layers -->
      <div class="smoke smoke-1"></div>
      <div class="smoke smoke-2"></div>
      <div class="smoke smoke-3"></div>

      <div
        class="hero-content"
        :style="{ transform: `perspective(900px) rotateX(${tiltY}deg) rotateY(${tiltX}deg)` }"
      >
        <h1 class="title">
          <span class="title-small">EL DE LA</span>
          <span class="title-big">SANTA</span>
        </h1>
        <p class="tagline">Securing the Bolsa</p>
        <div class="cta">
          <a class="btn" href="#media">Enter</a>
          <a class="btn btn-outline" href="#contact">Book Now</a>
        </div>
      </div>
      <div class="vignette"></div>
    </section>

    <section id="media" class="section">
      <h2 class="section-title">Latest Release</h2>
      <div class="media-card">
        <img class="media-cover" :src="coverUrl" alt="Album cover" />
        <div class="media-info">
          <h3>Securing The Bolsa</h3>
          <p class="artist">EL DE LA SANTA</p>
          <div class="links">
            <a class="btn small" href="#" target="_blank" rel="noopener">Spotify</a>
            <a class="btn small" href="#" target="_blank" rel="noopener">YouTube</a>
          </div>
        </div>
      </div>
    </section>

    <section id="about" class="section text">
      <h2 class="section-title">About</h2>
      <p>
        Música con vibra urbana y energía en vivo. Este template Vue 3 está diseñado
        para artistas: rápido, oscuro, con glow neón — listo para personalizar.
      </p>
    </section>

    <section id="contact" class="section">
      <h2 class="section-title">Contact</h2>
      <form class="contact" @submit.prevent="notify">
        <input class="input" type="text" placeholder="Your name" required />
        <input class="input" type="email" placeholder="Email" required />
        <textarea class="input" rows="4" placeholder="Your message" required></textarea>
        <button class="btn" type="submit">Send Request</button>
      </form>
      <p v-if="message" class="notice">{{ message }}</p>
    </section>

    <footer class="site-footer">© {{ year }} EL DE LA SANTA</footer>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import bg from './assets/background.webp'
import cover from './assets/dac4ec43-d69a-4521-97b8-ff37efee720c.jpg'
import video from './assets/santaintrovideo.mp4'

const bgUrl = bg
const coverUrl = cover
const videoUrl = video
const hasVideo = true

const tiltX = ref(0)
const tiltY = ref(0)
const message = ref('')

const onMove = (e) => {
  const rect = e.currentTarget.getBoundingClientRect()
  const x = (e.clientX - rect.left) / rect.width * 2 - 1
  const y = (e.clientY - rect.top) / rect.height * 2 - 1
  tiltX.value = x * 6
  tiltY.value = -y * 6
}

const notify = () => {
  message.value = 'Thanks! Your message is ready to be sent.'
  setTimeout(() => (message.value = ''), 3500)
}

const year = computed(() => new Date().getFullYear())
</script>

<style>
:root{
  --bg: #0a0a0a;
  --fg: #f8f8f8;
  --muted: #b3b3b3;
  --neon: #a8ff3a;
  --neon-soft: rgba(168,255,58,0.18);
}

*{ box-sizing: border-box; }
html, body, #app { height: 100%; }
body{
  margin: 0;
  background: var(--bg);
  color: var(--fg);
  font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
}

/* Header */
.site-header{
  position: fixed;
  top: 0; left: 0; right: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 22px;
  z-index: 20;
  background: linear-gradient(180deg, rgba(0,0,0,.55), rgba(0,0,0,0));
  backdrop-filter: blur(4px);
}
.brand{
  display: flex;
  align-items: baseline;
  gap: 10px;
  color: var(--fg);
  text-decoration: none;
}
.brand-small{ letter-spacing: .22em; font-size: 12px; opacity: .8; }
.brand-big{
  font-size: 20px;
  font-weight: 800;
  letter-spacing: .16em;
  text-shadow: 0 0 12px var(--neon-soft), 0 0 30px var(--neon-soft);
}
.nav a{
  margin-left: 18px;
  color: var(--muted);
  text-decoration: none;
  font-size: 14px;
}
.nav a:hover{ color: var(--fg); }

/* Hero */
.hero{
  position: relative;
  height: 92vh;
  overflow: hidden;
  background: #000;
}
.hero-video,.hero-bg{
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(.45) contrast(1.05) saturate(1.1);
}
.hero-bg{ object-position: center; }
.vignette{
  position: absolute;
  inset: 0;
  background: radial-gradient(60% 60% at 50% 50%, transparent 0%, rgba(0,0,0,.3) 60%, rgba(0,0,0,.9) 100%);
  pointer-events: none;
}

/* smoke / glow layers */
.smoke{
  position: absolute;
  width: 120vmax; height: 120vmax;
  left: 50%; top: 60%;
  transform: translate(-50%, -50%);
  background: radial-gradient(closest-side, var(--neon-soft), transparent 70%);
  filter: blur(70px);
  mix-blend-mode: screen;
  opacity: .35;
  animation: float 16s ease-in-out infinite alternate;
}
.smoke-2{ animation-duration: 22s; top: 40%; left: 40%; opacity: .25; }
.smoke-3{ animation-duration: 28s; top: 70%; left: 60%; opacity: .2; }
@keyframes float{ from{ transform: translate(-48%, -52%) scale(1); } to{ transform: translate(-52%, -48%) scale(1.1); } }

.hero-content{
  position: relative;
  z-index: 2;
  height: 100%;
  display: grid;
  place-content: center;
  text-align: center;
  padding-inline: 20px;
  will-change: transform;
}
.title{
  margin: 0 0 8px 0;
  line-height: .9;
}
.title-small{
  display: block;
  font-size: clamp(14px, 2.3vw, 20px);
  letter-spacing: .35em;
  opacity: .9;
}
.title-big{
  display: block;
  font-size: clamp(44px, 12vw, 160px);
  letter-spacing: .06em;
  font-weight: 900;
  color: #bfff52;
  text-shadow:
    0 0 10px var(--neon-soft),
    0 0 25px var(--neon-soft),
    0 0 60px rgba(168,255,58,0.35);
  filter: drop-shadow(0 15px 30px rgba(0,0,0,.6));
}
.tagline{
  margin: 6px 0 18px;
  color: var(--muted);
  letter-spacing: .2em;
  text-transform: uppercase;
  font-size: 12px;
}

/* Buttons */
.btn{
  display: inline-block;
  padding: 12px 18px;
  margin: 6px;
  border-radius: 999px;
  background: linear-gradient(180deg, var(--neon), #7ecb1a);
  color: #0b0f07;
  border: 1px solid rgba(168,255,58,.5);
  text-decoration: none;
  font-weight: 700;
  letter-spacing: .04em;
  box-shadow: 0 10px 30px rgba(168,255,58,.25);
  transition: transform .15s ease, box-shadow .2s ease, filter .2s ease;
}
.btn:hover{ transform: translateY(-2px); filter: brightness(1.05); box-shadow: 0 16px 36px rgba(168,255,58,.35); }
.btn-outline{
  background: rgba(0,0,0,.15);
  color: var(--fg);
  border: 1px solid rgba(168,255,58,.35);
  box-shadow: 0 10px 24px rgba(0,0,0,.35);
}
.btn.small{ padding: 8px 12px; font-size: 14px; }

/* Sections */
.section{
  padding: 72px 18px;
  max-width: 1100px;
  margin: 0 auto;
}
.section-title{
  margin: 0 0 18px;
  font-size: 28px;
  letter-spacing: .08em;
}
.text p{ color: var(--muted); max-width: 70ch; }

.media-card{
  display: grid;
  grid-template-columns: 1fr;
  gap: 18px;
  background: rgba(255,255,255,.02);
  border: 1px solid rgba(255,255,255,.06);
  border-radius: 16px;
  padding: 16px;
  box-shadow: 0 10px 40px rgba(0,0,0,.4);
}
@media (min-width: 780px){
  .media-card{ grid-template-columns: 360px 1fr; align-items: center; }
}
.media-cover{
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 12px;
}
.media-info h3{ margin: 0 0 6px; }
.media-info .artist{ color: var(--muted); margin: 0 0 12px; }
.links .btn{ margin-right: 8px; }

.contact{
  display: grid;
  gap: 10px;
  max-width: 560px;
}
.input{
  width: 100%;
  padding: 12px 14px;
  border-radius: 12px;
  background: rgba(255,255,255,.04);
  color: var(--fg);
  border: 1px solid rgba(255,255,255,.1);
}
.notice{
  margin-top: 10px;
  color: var(--muted);
}

.site-footer{
  text-align: center;
  padding: 36px 16px 60px;
  color: var(--muted);
  border-top: 1px solid rgba(255,255,255,.05);
}
</style>
