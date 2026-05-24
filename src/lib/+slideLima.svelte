<script>
    import { onMount } from 'svelte';
    import TypeIt from 'typeit';

    let showTerimakasih = $state(false);

    onMount(() => {
        setTimeout(() => {
            showTerimakasih = true;
            // Beri jeda mikro (50ms) setelah status reaktif berubah agar elemen p#trims siap dibaca TypeIt
            setTimeout(() => {
                new TypeIt("#trims", {
                    strings: ["Terimakasih."],
                    startDelay: 500,
                    speed: 150,
                    loop: false,
                    waitUntilVisible: true,
                }).go();
            }, 50);
        }, 1000); 
    });
</script>

<div class="container text-center" style="position: relative; top: 250px;">
    <div class="animate__bounceIn animate__animated animate__slow">
        <i class="fas fa-heart fa-5x text-danger"></i>
    </div>
    {#if showTerimakasih}
        <p id="trims" class="text-muted mt-4" style="font-size: 1.5rem; position: relative; top: 0;"></p>
    {/if}
</div>