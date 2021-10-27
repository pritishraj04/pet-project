<script>
  import Footer from "$lib/components/Footer.svelte";
  import Navbar from "$lib/components/Navbar.svelte";
  import "../app.css";
</script>

<section>
  <Navbar />
  <slot />
  <Footer />
</section>
