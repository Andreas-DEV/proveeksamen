<script lang="ts">
      import "../app.css";
      import Hero from "$lib/Hero.svelte";
      import Navbar from "$lib/Navbar.svelte";
      import About from "$lib/About.svelte";
      import Treatments from "$lib/Treatments.svelte";
      import Recommendation from "$lib/Recommendation.svelte";
      import Team from "$lib/Team.svelte";
      import Contact from "$lib/Contact.svelte";
      import Footer from "$lib/Footer.svelte";
</script>

<div class="mb-20 mt-10">
      <Navbar />
</div>
<Hero />
<About />
<Treatments />
<Recommendation />
<Team />
<Contact />
<Footer />
