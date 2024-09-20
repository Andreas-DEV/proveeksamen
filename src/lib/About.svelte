<script lang="ts">
    import butterfly from "$lib/assets/butterfly.png";
    import chinaRose from "$lib/assets/china-rose.png";
    import jasmine from "$lib/assets/jasmine.png";

    import { onMount } from "svelte";

    let aboutData = null;
    let error = null;

    onMount(async () => {
        try {
            const response = await fetch("http://localhost:5029/about");
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }
            aboutData = await response.json();
        } catch (e) {
            error = e.message;
        }
    });
</script>

<section class="relative py-16 px-4 sm:px-6 overflow-hidden">
    {#if aboutData}
    <div class="container mx-auto max-w-2xl text-center relative z-10">
      <img 
        class="absolute top-0 left-0 w-16 sm:w-24" 
        src={chinaRose} 
        alt="Decorative red flower"
      >
      <img 
        class="absolute bottom-0 right-0 w-16 sm:w-24" 
        src={jasmine} 
        alt="Decorative pink flower"
      >
      
      <div class="mb-4">
        <img src={butterfly} class="w-8 h-8 mx-auto" alt="Butterfly icon">
      </div>
      <h3 class="uppercase text-gray-500 text-sm mb-4">
        ABOUT OUR SPA CENTER
      </h3>
      <h2 class="text-3xl sm:text-4xl font-serif mb-6">{aboutData.title}</h2>
      <p class="text-gray-600 mb-8">{@html aboutData.content}</p>
  
      <button class="bg-[#ff827e] hover:text-black text-white px-8 py-3 rounded-full uppercase text-sm">Read More</button>
    </div>
    {/if}
  </section>
