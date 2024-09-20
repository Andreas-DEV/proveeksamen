<script>
    import { onMount } from 'svelte';
    import Navbar from '$lib/Navbar.svelte';
    import "../../app.css"
  
    let services = [];
    const apiUrl = 'http://localhost:5029/treatment';
  
    onMount(async () => {
      try {
        const response = await fetch(apiUrl);
        services = await response.json();
        console.log('Fetched services:', services);
      } catch (error) {
        console.error('Error fetching services:', error);
      }
    });
  
  </script>

  <div class="mt-10 mb-20">
    <Navbar/>
  </div>
  
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold mb-8 text-center uppercase">Our Services</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      {#each services as service}
        <div class="bg-white rounded-lg shadow-md overflow-hidden transition-transform duration-300 hover:scale-105">
          <img 
            src={"http://localhost:5029/images/treatment/" + service.image} 
            alt={service.title} 
            class="w-full h-48 object-cover" 
            
          />
          <div class="p-6">
            <h2 class="text-xl font-semibold mb-2">{service.title}</h2>
            <div class="text-gray-600">{@html service.content}</div>
          </div>
        </div>
      {/each}
    </div>
  </div>
  