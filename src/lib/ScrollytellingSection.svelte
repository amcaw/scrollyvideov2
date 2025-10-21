<script>
  import ScrollyVideo from '$lib/ScrollyVideo.svelte';
  import { base } from '$app/paths';
  import { onMount } from 'svelte';

  export let steps = [
    {
      title: "ScrollyVideo",
      text: "Sync video playback to scroll position with frame-perfect precision."
    },
    {
      title: "WebCodecs API",
      text: "Hardware-accelerated decoding for buttery smooth performance."
    },
    {
      title: "Framework Agnostic",
      text: "Works everywhere: React, Svelte, Vue, or plain HTML/JS."
    },
    {
      title: "Easy Integration",
      text: "Simple API with minimal configuration needed to get started."
    },
    {
      title: "Optimized Performance",
      text: "Smart caching and frame management for smooth scrolling."
    },
    {
      title: "Mobile Friendly",
      text: "Fully responsive design that works beautifully on all devices."
    },
    {
      title: "Customizable",
      text: "Control playback speed, transitions, and behavior."
    },
    {
      title: "Open Source",
      text: "Free to use with an active community and regular updates."
    },
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
          <h2 class="step-title">{step.title}</h2>
          <p class="step-text">{step.text}</p>

          {#if step.cta}
            <div class="cta-buttons">
              <a href="https://github.com/dkaoster/scrolly-video" class="button primary" target="_blank" rel="noopener">
                <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M10 0C4.477 0 0 4.477 0 10c0 4.42 2.865 8.17 6.839 9.49.5.092.682-.217.682-.482 0-.237-.008-.866-.013-1.7-2.782.603-3.369-1.34-3.369-1.34-.454-1.156-1.11-1.463-1.11-1.463-.908-.62.069-.608.069-.608 1.003.07 1.531 1.03 1.531 1.03.892 1.529 2.341 1.087 2.91.831.092-.646.35-1.086.636-1.336-2.22-.253-4.555-1.11-4.555-4.943 0-1.091.39-1.984 1.029-2.683-.103-.253-.446-1.27.098-2.647 0 0 .84-.269 2.75 1.025A9.578 9.578 0 0110 4.836c.85.004 1.705.114 2.504.336 1.909-1.294 2.747-1.025 2.747-1.025.546 1.377.203 2.394.1 2.647.64.699 1.028 1.592 1.028 2.683 0 3.842-2.339 4.687-4.566 4.935.359.309.678.919.678 1.852 0 1.336-.012 2.415-.012 2.743 0 .267.18.578.688.48C17.137 18.165 20 14.418 20 10c0-5.523-4.477-10-10-10z"/>
                </svg>
                GitHub
              </a>
              <a href="https://www.npmjs.com/package/scrolly-video" class="button secondary" target="_blank" rel="noopener">
                <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M0 0v20h20V0H0zm17 17H3V3h14v14z"/>
                  <path d="M5 5v10h5V7h2v8h3V5H5z"/>
                </svg>
                npm
              </a>
            </div>
          {/if}
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
    font-weight: 500;
    contain: layout style paint;
  }

  .step-title {
    font-size: 1.5rem;
    font-weight: 700;
    margin: 0 0 0.5rem 0;
    color: #000;
    letter-spacing: normal;
    line-height: 1.3;
  }

  .step-text {
    font-size: 1rem;
    color: #000;
    margin: 0;
    line-height: 1.5;
    font-weight: 500;
  }

  .cta-buttons {
    display: flex;
    gap: 0.75rem;
    margin-top: 1rem;
    flex-wrap: wrap;
  }

  .button {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    font-size: 0.875rem;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.2s ease;
    border: 1px solid #000;
  }

  .button.primary {
    background: #000;
    color: #fff;
  }

  .button.primary:hover {
    background: #333;
  }

  .button.secondary {
    background: #fff;
    color: #000;
  }

  .button.secondary:hover {
    background: #f5f5f5;
  }

  /* Responsive */
  @media (min-width: 769px) and (max-width: 1024px) {
    .step {
      justify-content: center;
    }
  }

  @media (max-width: 768px) {
    .step {
      justify-content: center;
      padding-left: 1rem;
      padding-right: 1rem;
    }

    .step-content {
      font-size: 0.9rem;
      padding: 0.75rem 1rem;
    }

    .step-title {
      font-size: 1.25rem;
    }

    .step-text {
      font-size: 0.9rem;
    }

    .cta-buttons {
      flex-direction: column;
      width: 100%;
    }

    .button {
      width: 100%;
      justify-content: center;
    }
  }
</style>
