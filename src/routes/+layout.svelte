<script>
  // No Lenis - using native scrolling for better cross-browser compatibility
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
    scroll-behavior: smooth;
  }

  :global(*) {
    box-sizing: border-box;
    outline: 1px solid red;
  }
</style>
