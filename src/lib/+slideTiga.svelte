<script>
    import { onMount } from 'svelte';
    import TypeIt from 'typeit';

    let { onComplete, showTapHint } = $props();

    onMount(() => {
        new TypeIt("#teks2", {
            strings: [
                "Dengan ataupun tanpaku, semoga semesta selalu membahagiakanmu bagimanapun caranya.", 
                " ", 
                "Barakallah fi umrik. Terima kasih sudah terus bertahan, bertumbuh, dan menjadi versi dirimu yang luar biasa sampai sejauh ini.", 
                " ", 
                "- Wish all you the best"
            ],
            startDelay: 500,
            speed: 75,
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