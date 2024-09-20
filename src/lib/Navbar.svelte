<script lang="ts">
    import logo from "$lib/assets/logo.png"
    import { onMount } from 'svelte';
   
    let isOpen = false;
    let isMobile = false;
   
    function toggleMenu() {
      isOpen = !isOpen;
    }
   
    onMount(() => {
      const mediaQuery = window.matchMedia('(max-width: 768px)');
      isMobile = mediaQuery.matches;
   
      const handleResize = (e) => {
        isMobile = e.matches;
        if (!isMobile) {
          isOpen = false;
        }
      };
   
      mediaQuery.addListener(handleResize);
   
      return () => {
        mediaQuery.removeListener(handleResize);
      };
    });
   </script>
   
   <header class="flex justify-between items-center p-4 max-w-6xl mx-auto">
     <img src={logo} alt="Logo" class="h-16">
     
     {#if isMobile}
       <button on:click={toggleMenu} class="text-2xl">
         ☰
       </button>
     {:else}
       <nav class="flex-grow">
         <ul class="uppercase flex items-center justify-center gap-6">
           <li><a class="font-medium hover:text-[#d3a49e]" href="/">home</a></li>
           <li><a class="font-medium hover:text-[#d3a49e]" href="/features">about</a></li>
           <li><a class="font-medium hover:text-[#d3a49e]" href="/features">feature</a></li>
           <li><a class="font-medium hover:text-[#d3a49e]" href="/services">service</a></li>
           <li><a class="font-medium hover:text-[#d3a49e]" href="#contact">contact</a></li>
         </ul>
       </nav>
     {/if}
   </header>
   
   {#if isMobile && isOpen}
     <nav class="fixed inset-0 bg-white z-50 p-4">
       <div class="flex justify-end">
         <button on:click={toggleMenu} class="text-2xl">
           ×
         </button>
       </div>
       <ul class="uppercase flex flex-col items-center gap-6 mt-12">
         <li><a href="/" on:click={toggleMenu}>home</a></li>
         <li><a href="/features" on:click={toggleMenu}>about</a></li>
         <li><a href="/features" on:click={toggleMenu}>feature</a></li>
         <li><a href="/services" on:click={toggleMenu}>service</a></li>
         <li><a href="#contact" on:click={toggleMenu}>contact</a></li>
       </ul>
     </nav>
   {/if}