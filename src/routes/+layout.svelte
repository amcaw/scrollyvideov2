<script>
  import { onMount, onDestroy } from 'svelte';
  import Lenis from 'lenis';
  import 'lenis/dist/lenis.css';

  let lenis;

  onMount(() => {
    // Initialize Lenis smooth scroll
    lenis = new Lenis({
      duration: 1.2,
      easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
      orientation: 'vertical',
      smoothWheel: true,
      wheelMultiplier: 1,
      touchMultiplier: 2,
    });

    // Animation frame loop
    function raf(time) {
      lenis.raf(time);
      requestAnimationFrame(raf);
    }
    requestAnimationFrame(raf);
  });

  onDestroy(() => {
    if (lenis) {
      lenis.destroy();
    }
  });
</script>

<slot />

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    background: #000;
    color: #fff;
    overflow-x: hidden;
    overscroll-behavior-y: none;
  }

  :global(html) {
    overscroll-behavior-y: none;
  }

  :global(html.lenis, html.lenis body) {
    height: auto;
  }

  :global(.lenis.lenis-smooth) {
    scroll-behavior: auto !important;
  }

  :global(.lenis.lenis-smooth [data-lenis-prevent]) {
    overscroll-behavior: contain;
  }

  :global(.lenis.lenis-stopped) {
    overflow: hidden;
  }

  :global(.lenis.lenis-scrolling iframe) {
    pointer-events: none;
  }

  :global(*) {
    box-sizing: border-box;
    outline: 1px solid red;
  }
</style>
