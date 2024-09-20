<script lang="ts">
    import { onMount } from "svelte";

    import test from "$lib/assets/team/1.jpg";
    import test2 from "$lib/assets/team/2.jpg";
    import test3 from "$lib/assets/team/3.jpg";

    

    interface TeamMember {
        id: number;
        firstname: string;
        lastname: string;
        role: string;
        image: string;
        // Add other properties as needed based on your API response
    }

    let teamMembers: TeamMember[] = [];
    let error: string | null = null;

    async function fetchTeamData() {
        try {
            const response = await fetch("http://localhost:5029/team");
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }
            teamMembers = await response.json();
            console.log(teamMembers);
        } catch (e) {
            error =
                e instanceof Error ? e.message : "An unknown error occurred";
        }
    }

    onMount(fetchTeamData);
</script>

<aside>
    <h3 class="text-center mt-20 mb-10 text-4xl">Experienced Team</h3>
    <p class=" w-[83ch] text-gray-500 text-lg mx-auto text-center mb-28">Lorem ipsum dolor sit amet consectetur adipisicing elit. Expedita fugit quas, optio suscipit sit quibusdam dicta tenetur alias! Repellat eius perspiciatis doloremque rem optio, dolores culpa veniam ducimus voluptates quasi pariatur sunt.</p>
</aside>

<section class="flex gap-5 justify-center my-10">
    {#each teamMembers as data}
        <div class="">
            <div class="relative flex justify-center items-center">
                <img class="h-[450px]" src={"http://localhost:5029/images/team/" + data.image} alt="" />
                <div
                    class="absolute bottom-0 bg-white w-full py-7 drop-shadow-xl text-center"
                >
                    <p>{data.firstname} {data.lastname}</p>
                    <p>{data.role}</p>
                </div>
            </div>
        </div>
    {/each}
</section>
