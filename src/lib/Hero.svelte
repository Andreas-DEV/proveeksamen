<script lang="ts">
    import logo from "$lib/assets/logo.png";
    import leaf from "$lib/assets/leaf.png";
    import jasmine from "$lib/assets/jasmine.png";
    import spaHero from "$lib/assets/spa.png";
    import butterfly from "$lib/assets/butterfly.png";
    import chinaRose from "$lib/assets/china-rose.png";
    import playIcon from "$lib/assets/icons/play-button.png";
    import { fade, scale, fly } from "svelte/transition";
    import { cubicOut } from "svelte/easing";
    import { createEventDispatcher } from "svelte";

    import { onMount } from "svelte";

    let showModal = false;
    const dispatch = createEventDispatcher();

    function toggleModal() {
        showModal = !showModal;
        if (!showModal) {
            dispatch("close");
        }
    }

    interface Hero {
        id: number;
        title1: string;
        title2: string;
        content: string;
        show: boolean;
    }

    let hero: Hero | null = null;
    let error: string | null = null;

    async function fetchHero() {
        try {
            const response = await fetch("http://localhost:5029/hero");
            if (!response.ok) {
                throw new Error("Network response was not ok");
            }
            const heroes: Hero[] = await response.json();
            const shownHeroes = heroes.filter((h) => h.show === true);

            if (shownHeroes.length === 0) {
                throw new Error("No hero found with show = true");
            } else if (shownHeroes.length > 1) {
                console.warn(
                    "Multiple heroes found with show = true. Using the first one.",
                );
            }

            hero = shownHeroes[0];
        } catch (err) {
            error =
                err instanceof Error
                    ? err.message
                    : "An unknown error occurred";
        }
    }

    onMount(fetchHero);
</script>

<section class="container mx-auto">
    <img
        src={spaHero}
        class="absolute top-0 right-0 w-[600px] lg:w-1/3 hidden xl:block"
        alt=""
    />
    <img
        src={leaf}
        class="absolute top-44 left-0 w-auto h-auto lg:block hidden"
        alt=""
    />

    <section
        class="container sm:mx-auto lg:mx-0 my-16 max-w-screen-xl xl:-ms-16 2xl:ms-16"
    >
        <div
            class="container mx-auto px-4 pt-56 flex justify-center items-start -mt-16"
        >
            <div class="w-full lg:w-1/2">
                {#if hero}
                    <h3 class="text-pink-400 uppercase mb-2">
                        {hero.title1}
                    </h3>
                    <h1 class="text-5xl font-bold mb-4">{hero.title2}</h1>
                    <p class="text-gray-600 mb-8">{hero.content}</p>
                    <div
                        class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4"
                    >
                        <button
                            class="bg-[#ff827e] hover:text-black text-white px-6 py-3 rounded-sm uppercase"
                            >Reserve now</button
                        >
                        <button
                            on:click={toggleModal}
                            class="flex items-center space-x-2"
                        >
                            <img
                                src={playIcon}
                                alt="Play"
                                class="w-11 h-11 p-3 bg-pink-100 rounded-full"
                            />
                            <span class="hover:text-[#d3a49e]">Watch our story</span>
                        </button>
                        {#if showModal}
                            <div
                                class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 sm:p-6 md:p-8"
                                on:click={toggleModal}
                                transition:fade={{ duration: 200 }}
                            >
                                <div
                                    class="relative w-full max-w-5xl aspect-video bg-white rounded-lg shadow-2xl overflow-hidden"
                                    on:click|stopPropagation
                                    transition:fly={{
                                        y: 50,
                                        duration: 300,
                                        easing: cubicOut,
                                    }}
                                >
                                    <button
                                        on:click={toggleModal}
                                        class="absolute top-3 right-3 text-gray-400 hover:text-gray-600 transition-colors z-10"
                                    >
                                        <svg
                                            xmlns="http://www.w3.org/2000/svg"
                                            class="h-6 w-6"
                                            fill="none"
                                            viewBox="0 0 24 24"
                                            stroke="currentColor"
                                        >
                                            <path
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                stroke-width="2"
                                                d="M6 18L18 6M6 6l12 12"
                                            />
                                        </svg>
                                    </button>
                                    <iframe
                                        src="https://www.youtube.com/embed/yCPw4JIQ6yg"
                                        frameborder="0"
                                        allow="encrypted-media; picture-in-picture"
                                        allowfullscreen
                                        class="absolute inset-0 w-full h-full"
                                    ></iframe>
                                </div>
                            </div>
                        {/if}
                    </div>
                {/if}
            </div>
        </div>
    </section>
</section>
