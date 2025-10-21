# ScrollyVideo - Svelte Demo

A responsive scrollable video component for Svelte with optimized performance.

## Features

- 🎬 Scroll-driven video playback
- ⚡ WebCodecs API for buttery smooth performance
- 🎨 Beautiful scrollytelling layout
- 📱 Fully responsive
- 🚀 Optimized component with smart prop diffing

## Getting Started

### Install Dependencies

```bash
npm install
```

### Run Development Server

```bash
cd demos/svelte
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

## Project Structure

```
scrolly-video-main/
├── src/
│   ├── ScrollyVideo.svelte    # Optimized Svelte component
│   ├── ScrollyVideo.js         # Core video controller
│   ├── videoDecoder.js         # WebCodecs implementation
│   └── utils.js                # Helper utilities
└── demos/
    └── svelte/                 # Demo application
        └── src/
            └── routes/
                └── +page.svelte # Main demo page
```

## Component Usage

```svelte
<script>
  import ScrollyVideo from './path/to/ScrollyVideo.svelte';
</script>

<ScrollyVideo src="https://example.com/video.mp4" />
```

## Performance Optimizations

- ✅ Smart prop diffing - no JSON.stringify
- ✅ Preserves WebCodecs decoded frames
- ✅ Hot-updates non-critical props
- ✅ Efficient reactive blocks

## License

MIT

---

Created with [Claude Code](https://claude.com/claude-code)
