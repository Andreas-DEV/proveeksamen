<script lang="ts">
    import quoteIcon from "$lib/assets/quote.png";
    import { onMount } from "svelte";
    import { fade } from "svelte/transition";
    import { quintOut } from "svelte/easing";

    interface Recommendation {
        name: string;
        title: string;
        content: string;
        image: string;
    }

    let recommendations: Recommendation[] = [];
    let currentIndex = 0;

    async function fetchRecommendations() {
        try {
            const response = await fetch(
                "http://localhost:5029/recommendation",
            );
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }
            recommendations = await response.json();
            console.log(recommendations);
        } catch (error) {
            console.error("Error fetching recommendations:", error);
        }
    }

    function nextSlide() {
        currentIndex = (currentIndex + 1) % recommendations.length;
    }

    function prevSlide() {
        currentIndex =
            (currentIndex - 1 + recommendations.length) %
            recommendations.length;
    }

    onMount(() => {
        fetchRecommendations();
    });
</script>

<section
    class="flex flex-col bg-red-50 text-center justify-center items-center p-8 h-[500px] relative"
>
    {#if recommendations.length > 0}
        <div class="relative w-full max-w-3xl relative">
            <div
                in:fade={{ duration: 300, easing: quintOut }}
                out:fade={{ duration: 300 }}
            >
                <img
                    class="w-12 mx-auto my-10"
                    src={quoteIcon}
                    alt="Quote icon"
                />
                <p class="text-lg mb-6">
                    {recommendations[currentIndex].content}
                </p>
                <div class="flex flex-col items-center">
                    <img
                        class="w-16 h-16 rounded-full mb-2"
                        src={"http://localhost:5029/images/recommendation/" + recommendations[currentIndex].image}
                        alt={recommendations[currentIndex].name}
                    />
                    <div class="flex items-center justify-center">
                        <p class="text-xl font-semibold mr-2">
                            {recommendations[currentIndex].name},
                        </p>
                        <p class="text-sm">
                            {recommendations[currentIndex].title}
                        </p>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex justify-center mt-8 absolute bottom-8">
            {#each recommendations as _, i}
                <button
                    class="w-3 h-3 rounded-full mx-1 focus:outline-none"
                    class:bg-red-500={i === currentIndex}
                    class:bg-red-300={i !== currentIndex}
                    on:click={() => (currentIndex = i)}
                />
            {/each}
        </div>
    {:else}
        <p>Loading recommendations...</p>
    {/if}
</section>
