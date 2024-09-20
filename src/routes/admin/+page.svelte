<script>
    import { onMount } from "svelte";
    import "../../app.css";
    import Navbar from "$lib/Navbar.svelte";

   
    let treatments = [];
    let error = "";

    onMount(async () => {
        await fetchTreatments();
    });

    async function fetchTreatments() {
        try {
            const response = await fetch("http://localhost:5029/treatment");
            if (response.ok) {
                treatments = await response.json();
            } else {
                throw new Error("Failed to fetch treatments");
            }
        } catch (err) {
            error = "Error fetching treatments. Please try again.";
            console.error("Error:", err);
        }
    }

    async function deleteTreatment(id) {
        if (confirm("Er du sikker på du vil slette dette?")) {
            try {
                const response = await fetch(
                    `http://localhost:5029/treatment/admin/${id}`,
                    {
                        method: "DELETE",
                    },
                );
                if (response.ok) {
                    treatments = treatments.filter((t) => t._id !== id);
                } else {
                    throw new Error("Failed to delete treatment");
                }
            } catch (err) {
                error = "Error deleting treatment. Please try again.";
                console.error("Error:", err);
            }
        }
    }

    let title = "";
    let content = "";
    let image = null;
    let submitting = false;
    let message = "";

    async function handleSubmitTreatment() {
        submitting = true;
        message = "";

        const formData = new FormData();
        formData.append("title", title);
        formData.append("content", content);
        if (image) {
            formData.append("image", image);
        }

        try {
            const response = await fetch(
                "http://localhost:5029/treatment/admin",
                {
                    method: "POST",
                    body: formData,
                },
            );

            if (response.ok) {
                message = "Post submitted successfully!";
                title = "";
                content = "";
                image = null;
            } else {
                message = "Error submitting post. Please try again.";
            }
        } catch (error) {
            console.error("Error:", error);
            message = "An error occurred. Please try again.";
        } finally {
            submitting = false;
        }
    }

    function handleFileChange(event) {
        const file = event.target.files[0];
        if (file) {
            image = file;
        }
    }
</script>

<div class="mt-10 mb-20">
    <Navbar />
</div>

<!-- TREATMENTS -->
<section>
    <form
        on:submit|preventDefault={handleSubmitTreatment}
        class="max-w-md mx-auto mt-8 p-6 bg-white rounded-lg shadow-md"
    >
        <div class="mb-4">
            <label
                for="title"
                class="block text-gray-700 text-sm font-bold mb-2">Title</label
            >
            <input
                type="text"
                id="title"
                bind:value={title}
                required
                class="w-full px-3 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
        </div>

        <div class="mb-4">
            <label
                for="content"
                class="block text-gray-700 text-sm font-bold mb-2"
                >Content</label
            >
            <textarea
                id="content"
                bind:value={content}
                required
                class="w-full px-3 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 h-32"
            ></textarea>
        </div>

        <div class="mb-4">
            <label
                for="image"
                class="block text-gray-700 text-sm font-bold mb-2">Image</label
            >
            <input
                type="file"
                id="image"
                on:change={handleFileChange}
                accept="image/*"
                class="w-full px-3 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
        </div>

        <button
            type="submit"
            disabled={submitting}
            class="w-full bg-blue-500 text-white font-bold py-2 px-4 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50"
        >
            {submitting ? "Opretter..." : "Opret"}
        </button>

        {#if message}
            <p
                class="mt-4 text-center {message.includes('Error')
                    ? 'text-red-500'
                    : 'text-green-500'}"
            >
                {message}
            </p>
        {/if}
    </form>
</section>

<div class="max-w-4xl mx-auto mt-8 p-6 bg-white rounded-lg shadow-md">
    <h2 class="text-2xl font-bold mb-4">Treatments</h2>

    {#if error}
        <p class="text-red-500 mb-4">{error}</p>
    {/if}

    {#if treatments.length === 0}
        <p class="text-gray-500">No treatments found.</p>
    {:else}
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            {#each treatments as treatment (treatment._id)}
                <div class="border rounded-lg p-4 flex flex-col">
                    <h3 class="text-xl font-semibold mb-2">
                        {treatment.title}
                    </h3>
                    <p class="text-gray-600 mb-2 flex-grow">
                        {@html treatment.content}
                    </p>
                    {#if treatment.image}
                        <img
                            src={"http://localhost:5029/images/treatment/" +
                                treatment.image}
                            alt={treatment.title}
                            class="w-full h-40 object-cover mb-2 rounded"
                        />
                    {/if}
                    <button
                        on:click={() => deleteTreatment(treatment._id)}
                        class="bg-red-500 text-white font-bold py-2 px-4 rounded hover:bg-red-600 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50"
                    >
                        Delete
                    </button>
                </div>
            {/each}
        </div>
    {/if}
</div>

<!-- ABOUT -->
