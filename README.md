# EL DE LA SANTA — Vue 3 Template

Dark, neon-glow Vue 3 single-page template with a video background hero and an album card.
Assets included: background.webp, dac4ec43-d69a-4521-97b8-ff37efee720c.jpg, santaintrovideo.mp4.

## 🚀 Quick start

```bash
npm install
npm run dev
```

Build for production:

```bash
npm run build
npm run preview
```

## 🧩 Notes
- The hero uses your `santaintrovideo.mp4` as the background (muted + loop). If you prefer a static hero, delete the `video` import in `App.vue` and set `hasVideo=false`.
- All styling is simple CSS (no CDN). You can add Tailwind later if you want.
- Replace links in the **Media** section with your real Spotify/YouTube URLs.
- Update colors by changing CSS variables at the top of `<style>` in `App.vue`.
