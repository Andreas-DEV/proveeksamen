<script lang="ts">
    import Navbar from "$lib/Navbar.svelte";
    import { onMount } from "svelte";
    import { fade } from "svelte/transition";

    let visible = false;

    onMount(() => {
        visible = true;
    });
</script>

<div class="mt-10 mb-20">
    <Navbar />
</div>

<section class="">
    <div>
        <div
            class="min-h-screen  p-8"
        >
            {#if visible}
                <div
                    class="max-w-4xl mx-auto bg-white rounded-lg shadow-xl overflow-hidden"
                    transition:fade
                >
                    <header class="bg-purple-600 text-white p-6 text-center">
                        <h1 class="text-4xl font-bold mb-2">
                            Copenhagen Beauty 2024
                        </h1>
                        <p class="text-xl">15. - 17. november, Bella Center</p>
                    </header>

                    <main class="p-6">
                        <p class="text-gray-700 mb-6">
                            Copenhagen Beauty 2024 vender tilbage til Bella
                            Center fra 15. til 17. november, og
                            skønhedsentusiaster fra hele Norden kan se frem til
                            en begivenhedsrig weekend. Dette årlige event lover
                            at blive større og mere innovativt end nogensinde
                            før.
                        </p>

                        <h2 class="text-2xl font-semibold mb-4 text-purple-600">
                            Besøgende kan glæde sig til:
                        </h2>

                        <ul class="space-y-4">
                            {#each ["Fremvisning af de nyeste trends: Over 200 udstillere vil præsentere de seneste innovationer inden for makeup, hudpleje og hårprodukter.", "Bæredygtig skønhedszone: Et dedikeret område for økologiske og miljøvenlige produkter, hvor besøgende kan opdage fremtidens grønne skønhedsløsninger.", "Masterclasses med kendte makeupartister: Lær tricks og teknikker fra nogle af branchens mest respekterede navne.", "Tech i skønhedsindustrien: Oplev demonstrationer af cutting-edge teknologi, herunder en ny AI-drevet app til personlig hudanalyse.", "Paneldiskussioner: Hør eksperter debattere fremtidens skønhedstrends og industriens udfordringer.", "Eksklusive lanceringer: Vær blandt de første til at se og prøve nye produkter før de rammer butikkerne.", "Netværksmuligheder: Mød ligesindede skønhedsentusiaster og professionelle fra hele Skandinavien."] as item, i}
                                <li class="flex items-start">
                                    <span
                                        class="inline-flex items-center justify-center h-6 w-6 rounded-full bg-purple-500 text-white font-semibold text-sm mr-3 mt-0.5 flex-shrink-0"
                                        >{i + 1}</span
                                    >
                                    <span class="text-gray-700">{item}</span>
                                </li>
                            {/each}
                        </ul>

                        <div class="mt-8 bg-pink-100 p-6 rounded-lg">
                            <h3
                                class="text-xl font-semibold mb-2 text-pink-700"
                            >
                                Forventninger og billetter
                            </h3>
                            <p class="text-gray-700 mb-4">
                                Arrangørerne forventer rekorddeltagelse med over
                                50.000 besøgende i løbet af de tre dage. Tidlige
                                tilmeldinger tyder på, at Copenhagen Beauty 2024
                                bliver årets must-attend event for alle med
                                interesse i skønhedsindustrien.
                            </p>
                            <p class="text-gray-700 mb-4">
                                Billetter bliver sat til salg fra 1. september
                                på eventets officielle hjemmeside. Der vil være
                                et begrænset antal VIP-billetter, som giver
                                adgang til eksklusive workshops og en goodiebag
                                med luksusprodukter.
                            </p>
                            <button
                                class="bg-pink-500 hover:bg-pink-600 text-white font-bold py-2 px-4 rounded transition duration-300"
                            >
                                Køb billetter nu
                            </button>
                        </div>
                    </main>
                </div>
            {/if}
        </div>
    </div>
</section>
