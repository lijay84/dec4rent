<script>
  import Hero from "./Hero.svelte";
  let banner = {
    title: "noleggia sci e snowboard online",
    subtitle:
      "nei nostri negozi o presso i partner nelle migliori località d'italia",
    discount: 50,
    bgImage: "https://rent.decathlon.it/background.9f83f538e01e3e7338bb.webp"
  };
</script>

<style>
  body * {
    font-family: "Roboto Condensed", sans-serif;
  }
</style>

<main>
  <Hero heroProps={banner} />
</main>
