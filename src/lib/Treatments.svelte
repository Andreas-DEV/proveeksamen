<script lang="ts">
    import one from "$lib/assets/extra_procedures_etc/4.jpg";
    import two from "$lib/assets/extra_procedures_etc/5.jpg";
    import three from "$lib/assets/extra_procedures_etc/6.jpg";
    import four from "$lib/assets/extra_procedures_etc/7.jpg";
    import icon from "$lib/assets/icons/1.png";

    import firstCard from "$lib/assets/extra_procedures_etc/1.jpg";
    import secondCard from "$lib/assets/extra_procedures_etc/2.jpg";
    import thirdCard from "$lib/assets/extra_procedures_etc/3.jpg";
</script>

<section class="mt-36 mb-20 flex justify-center">
    <ul class="flex gap-1">
        {#each [one, two, three, four] as img}
            <li class="relative group ">
                <img src={img} alt="" class="w-full h-full object-cover rounded-sm" />
                <div
                    class="absolute inset-0 bg-red-400 bg-opacity-80 flex flex-col items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                >
                    <img src={icon} alt="" />
                    <span class="text-white text-sm font-medium"
                        >Body Treatment</span
                    >
                </div>
            </li>
        {/each}
    </ul>
</section>

<!-- POPULAR PROCEDURES -->
<section class="">
    <div class="text-center">
        <h2 class="text-4xl my-10">Popular Procedures</h2>

        <p class="text-sm text-gray-400">
            To doesn't his appear replenish together called he of mad place
            won't wherein blessed second every wherein <br /> were meat kind wherein
            and martcin
        </p>
    </div>

    <!-- CARDS -->
    <div class="flex gap-10 items-center justify-center my-10">
        <div class="border w-[350px] flex flex-col items-center p-4">
            <img class="" src={firstCard} alt="" />
            <div class="text-center">
                <h3 class="text-xl my-4">Massage Therapy</h3>
                <p class="text-sm my-4">
                    Living winged said you darkness you're divide gathered and
                    bring one seasons face great dr Waters firmament place
                    which..
                </p>
                <button
                    class="bg-neutral-800 text-white px-8 py-3 uppercase rounded-full mb-10 hover:bg-[#ff827e]"
                    >read more</button
                >
            </div>
        </div>
        <div class="border w-[350px] flex flex-col items-center p-4">
            <img class="" src={secondCard} alt="" />
            <div class="text-center">
                <h3 class="text-xl my-4">Massage Therapy</h3>
                <p class="text-sm my-4">
                    Living winged said you darkness you're divide gathered and
                    bring one seasons face great dr Waters firmament place
                    which..
                </p>
                <button
                    class="bg-neutral-800 text-white px-8 py-3 uppercase rounded-full mb-10 hover:bg-[#ff827e]"
                    >read more</button
                >
            </div>
        </div>
        <div class="border w-[350px] flex flex-col items-center p-4">
            <img class="" src={thirdCard} alt="" />
            <div class="text-center">
                <h3 class="text-xl my-4">Massage Therapy</h3>
                <p class="text-sm my-4">
                    Living winged said you darkness you're divide gathered and
                    bring one seasons face great dr Waters firmament place
                    which..
                </p>
                <button
                    class="bg-neutral-800 text-white px-8 py-3 uppercase rounded-full mb-10 hover:bg-[#ff827e]"
                    >read more</button
                >
            </div>
        </div>
    </div>
</section>
