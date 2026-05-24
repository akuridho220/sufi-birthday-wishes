<script>
    import { onMount } from 'svelte';
    import TypeIt from 'typeit';

    let { onComplete, showTapHint } = $props();

    onMount(() => {
        new TypeIt("#teks2", {
            strings: [
                "Entah pas kamu lagi sendiri, lagi seru-seruan bareng temen-temen, atau pas kita lagi ngobrol, semoga semesta selalu membahagiakanmu.", 
                " ", 
                "Barakallah fi umrik. Terima kasih sudah terus bertahan, bertumbuh, dan menjadi versi dirimu yang luar biasa sampai sejauh ini.", 
                " ", 
                "- With Love, Mas Ridho"
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

<div class="slides paper animate__fadeInRight animate__animated">
    <div class="paper-content">
        <p id="teks2" class="teks"></p>
    </div>
</div>

{#if showTapHint}
    <p class="animate__animated animate__fadeIn animate__infinite animate__slow text-muted">
        Ketuk layarnya ya...
    </p>
{/if}