<script>
  export let title = "Lorem Ipsum";
  export let paragraphs = 3;
</script>

<section class="lorem-section">
  <div class="lorem-container">
    <h1>{title}</h1>
    {#each Array(paragraphs) as _, i}
      {#if i === 0}
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
        </p>
      {:else if i === 1}
        <p>
          Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.
        </p>
      {:else}
        <p>
          Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.
        </p>
      {/if}
    {/each}
  </div>
</section>

<style>
  .lorem-section {
    padding: 8rem 2rem;
    background: #000;
    color: #fff;
  }

  .lorem-container {
    max-width: 800px;
    margin: 0 auto;
  }

  h1 {
    font-size: 3rem;
    font-weight: 700;
    margin: 0 0 2rem 0;
    letter-spacing: -0.02em;
    line-height: 1.2;
  }

  p {
    font-size: 1.125rem;
    line-height: 1.8;
    margin: 0 0 1.5rem 0;
    color: rgba(255, 255, 255, 0.8);
  }

  p:last-child {
    margin-bottom: 0;
  }

  @media screen and (max-width: 768px) {
    .lorem-section {
      padding: 4rem 1.5rem;
    }

    h1 {
      font-size: 2rem;
    }

    p {
      font-size: 1rem;
      line-height: 1.6;
    }
  }
</style>
