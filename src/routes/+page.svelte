<script>
  import ScrollytellingSection from '$lib/ScrollytellingSection.svelte';
  import LoremSection from '$lib/LoremSection.svelte';
</script>

<svelte:head>
  <title>ScrollyVideo - Responsive Scrollable Videos</title>
  <meta name="description" content="Responsive scrollable videos without obscure video encoding requirements" />
</svelte:head>

<LoremSection title="Introduction" paragraphs={3} />

<ScrollytellingSection />

<LoremSection title="Conclusion" paragraphs={3} />


