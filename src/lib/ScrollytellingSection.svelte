<script>
  import ScrollyVideo from '$lib/ScrollyVideo.svelte';
  import { base } from '$app/paths';
  import { onMount } from 'svelte';

  export let steps = [
    "This is a scroll-driven video player that synchronizes video playback with your scroll position in real-time.",
    "As you scroll down, the video plays forward frame-by-frame; scroll up and it plays backward smoothly.",
    "Uses WebCodecs API for hardware-accelerated video decoding, delivering buttery smooth 60fps performance.",
    "Lenis smooth scrolling library adds momentum-based physics for a natural, fluid scrolling experience.",
    "The modular component architecture separates concerns: ScrollytellingSection handles layout, ScrollyVideo manages playback.",
    "Dynamic height calculation automatically measures content and adjusts the video container height for perfect synchronization.",
    "Each content step has natural auto-height with 100vh spacing ensuring smooth transitions between sections.",
    "Fully responsive across all devices with optimized mobile styles and consistent content width."
  ];
  export let videoSrc = `${base}/output.mp4`;
  export let transitionSpeed = 12;
  export let frameThreshold = 0.05;
  export let useWebCodecs = true;

  let foregroundElement;
  // Approximate fallback height before measuring: 50vh top margin + (steps × ~150vh each) + 100vh bottom
  let scrollHeight = `${50 + steps.length * 150 + 100}vh`;

  onMount(() => {
    if (!foregroundElement) return;

    const updateHeight = () => {
      scrollHeight = `${foregroundElement.offsetHeight}px`;
    };

    updateHeight();
    window.addEventListener('resize', updateHeight);

    return () => window.removeEventListener('resize', updateHeight);
  });
</script>

<section class="scrollytelling-container" style="--scroll-height: {scrollHeight}">
  <div class="video-scroll-container">
    <ScrollyVideo
      src={videoSrc}
      {transitionSpeed}
      {frameThreshold}
      {useWebCodecs}
    />
  </div>

  <div class="overlay"></div>

  <div class="foreground" bind:this={foregroundElement}>
    {#each steps as step, index}
      <div class="step" data-step={index}>
        <div class="step-content">
          <p class="step-text">{step}</p>
        </div>
      </div>
    {/each}
  </div>
</section>

<style>
  .scrollytelling-container {
    position: relative;
    min-height: 100vh;
  }

  .video-scroll-container {
    height: var(--scroll-height);
    position: relative;
    will-change: transform;
  }

  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.1);
    pointer-events: none;
    z-index: 5;
  }

  .foreground {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 10;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    pointer-events: none;
  }

  .step {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    position: relative;
    width: 100%;
    height: auto;
    padding-left: 2rem;
    margin-bottom: 100vh;
  }

  .step:first-child {
    margin-top: 50vh;
  }

  .step:last-child {
    margin-bottom: 100vh;
  }

  .step-content {
    background: #fff;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border-radius: 4px;
    color: #000;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    padding: 1rem 1.5rem;
    width: 100%;
    max-width: 500px;
    pointer-events: auto;
    contain: layout style paint;
  }

  .step-text {
    font-size: 1.125rem;
    color: #000;
    margin: 0;
    line-height: 1.6;
    font-weight: 400;
    word-wrap: break-word;
    overflow-wrap: break-word;
  }

  /* Responsive */
  @media (max-width: 768px) {
    .step {
      justify-content: center;
      padding-left: 0;
    }

    .step-content {
      padding: 1rem;
      width: calc(100% - 2rem);
      max-width: calc(100% - 2rem);
      margin: 0 1rem;
    }

    .step-text {
      font-size: 1rem;
      line-height: 1.5;
    }
  }
</style>
