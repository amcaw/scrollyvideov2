# ScrollyVideo - Svelte

A beautiful, performant scroll-driven video component for SvelteKit with smooth scrolling and optimized playback.

## ✨ Features

- 🎬 **Scroll-driven video playback** - Video progress synced to scroll position
- ⚡ **WebCodecs API** - Hardware-accelerated video decoding for buttery smooth performance
- 🎯 **Lenis smooth scrolling** - Ultra-smooth, momentum-based scroll experience
- 🎨 **Beautiful scrollytelling layout** - Dynamic steps with clean transitions
- 📱 **Fully responsive** - Works perfectly on mobile, tablet, and desktop
- 🚀 **Performance optimized** - CSS containment, GPU acceleration, efficient rendering
- 🎛️ **Highly customizable** - Control transition speed, frame threshold, and more
- 📏 **Dynamic spacing** - Configurable gaps between content steps

## 🚀 Quick Start

### Install Dependencies

```bash
npm install
```

### Run Development Server

```bash
npm run dev
```

Open [http://localhost:5174](http://localhost:5174) in your browser.

### Build for Production

```bash
npm run build
```

## 📁 Project Structure

```
scrollyvideov2/
├── src/
│   ├── lib/
│   │   ├── ScrollytellingSection.svelte # Complete scrollytelling component
│   │   ├── ScrollyVideo.svelte          # Video playback component
│   │   ├── ScrollyVideo.js              # Core video controller
│   │   ├── videoDecoder.js              # WebCodecs implementation
│   │   ├── utils.js                     # Helper utilities
│   │   └── LoremSection.svelte          # Example section component
│   ├── routes/
│   │   ├── +layout.svelte               # Global layout with Lenis scroll
│   │   ├── +layout.js                   # SvelteKit layout config
│   │   └── +page.svelte                 # Demo page
│   └── app.html                         # HTML template
├── static/
│   ├── output.mp4                       # Demo video file
│   └── poster.jpg                       # Video poster image
├── VIDEO_ENCODING.md                    # Video encoding guide
└── package.json
```

## 🎬 Component Usage

### Basic Usage

```svelte
<script>
  import ScrollyVideo from '$lib/ScrollyVideo.svelte';
</script>

<ScrollyVideo src="/path/to/video.mp4" />
```

### With Custom Props

```svelte
<ScrollyVideo
  src="/path/to/video.mp4"
  transitionSpeed={12}
  frameThreshold={0.05}
  useWebCodecs={true}
/>
```

### Available Props

- **`src`** (string) - Path to your video file
- **`transitionSpeed`** (number, default: 8) - Controls scroll smoothness (higher = smoother)
- **`frameThreshold`** (number, default: 0.1) - Frame update sensitivity (lower = more updates)
- **`useWebCodecs`** (boolean, default: true) - Enable WebCodecs for better performance
- **`cover`** (boolean, default: true) - Video covers container
- **`sticky`** (boolean, default: true) - Video stays fixed while scrolling
- **`trackScroll`** (boolean, default: true) - Sync video to scroll position

## 🎥 Video Encoding

For optimal performance, encode your videos using the provided ffmpeg command:

```bash
ffmpeg -i input.mp4 -c:v libx264 -preset medium -crf 25 \
  -vf "scale='min(1280,iw)':'min(720,ih)':force_original_aspect_ratio=decrease" \
  -g 30 -pix_fmt yuv420p -profile:v main -movflags +faststart -an output.mp4
```

See [VIDEO_ENCODING.md](./VIDEO_ENCODING.md) for detailed encoding instructions and optimization tips.

## ⚡ Performance Features

- **WebCodecs API** - Hardware-accelerated video decoding
- **CSS Containment** - Isolated rendering for better performance
- **GPU Acceleration** - `will-change` hints for smooth compositing
- **Smart Prop Diffing** - Only updates when props actually change
- **Lenis Integration** - Smooth, performant scrolling library
- **Fixed Step Heights** - Consistent 100vh spacing for predictable scrolling

## 🎨 Customization

### Dynamic Steps

The demo includes 8 customizable content steps. Modify the `steps` array in `src/lib/ScrollytellingSection.svelte`:

```svelte
export let steps = [
  "Your first step description",
  "Your second step description",
  // Add more steps...
];
```

The scroll height automatically adjusts based on the number of steps.

### Styling

All styles are in `src/lib/ScrollytellingSection.svelte`. Key classes:
- `.step` - Individual step container
- `.step-content` - Content box styling
- `.step-text` - Text styling
- `.foreground` - Steps overlay container
- `.video-scroll-container` - Video container

### Smooth Scrolling

Lenis configuration in `src/routes/+layout.svelte`:

```javascript
lenis = new Lenis({
  duration: 1.2,              // Scroll duration
  easing: (t) => ...,         // Easing function
  smoothWheel: true,          // Smooth mouse wheel
  wheelMultiplier: 1,         // Wheel sensitivity
  touchMultiplier: 2,         // Touch sensitivity
});
```

## 🛠️ Tech Stack

- **SvelteKit** - Full-stack framework
- **Vite** - Build tool
- **Lenis** - Smooth scrolling
- **WebCodecs API** - Video decoding
- **H.264** - Video codec

## 📱 Browser Support

- Chrome/Edge 94+ (WebCodecs support)
- Safari 16.4+
- Firefox 100+ (with flag enabled)

Fallback to standard video decoding on unsupported browsers.

## 🐛 Troubleshooting

**Video not loading?**
- Check the video file path in `static/`
- Ensure video is H.264 encoded with `-movflags +faststart`
- Check browser console for errors

**Choppy scrolling?**
- Reduce `transitionSpeed` (try 8 instead of 12)
- Increase `frameThreshold` (try 0.1 instead of 0.05)
- Use lower resolution video (540p instead of 720p)

**Video not syncing with scroll?**
- Ensure `trackScroll={true}` is set
- Check that video container and foreground heights match
- Verify scroll height calculation is correct

## 📄 License

MIT

## 🙏 Credits

Inspired by [scrolly-video](https://github.com/dkaoster/scrolly-video) by [@dkaoster](https://github.com/dkaoster)

Built with [Claude Code](https://claude.com/claude-code)

---

**Live Demo:** [View on GitHub Pages](#)
