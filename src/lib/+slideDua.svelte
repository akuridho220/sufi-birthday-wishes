<script>
    import { onMount } from 'svelte';
    import TypeIt from 'typeit';

    let { onComplete, showTapHint } = $props();

    onMount(() => {
        // Berjalan instan tanpa setTimeout pelindung karena elemen dipastikan sudah ada di DOM
        new TypeIt("#teks1", {
            strings: [
                "Selamat ulang tahun Sufi Sayang! Selamat bertambah tua, hehee.", 
                "Terimakasih sudah hadir ke dunia 23 tahun yang laluu.", 
                "Semoga kamu selalu dikelilingi oleh hal-hal baik, dan diberi kelancaran untuk setiap target yang lagi kamu perjuangkan.", 
                "Semoga di umur yang baru ini kamu makin sukses, dilancarkan rezekinya, dan dimudahkan segala urusannyaa.", 
                "Semoga harimu selalu hangat, di manapun kamu berada."
            ],
            startDelay: 500,
            speed: 100,
            waitUntilVisible: true,
            afterComplete: function (instance) {
                onComplete();
                instance.destroy(); 
            }
        }).go();
    });
</script>

<div class="paper animate__zoomInDown animate__animated animate__slow">
    <div class="paper-content">
        <p id="teks1" class="teks"></p>
    </div>
</div>

{#if showTapHint}
    <p class="animate__animated animate__fadeIn animate__infinite animate__slow text-muted">
        Ketuk layarnya ya...
    </p>
{/if}