<script>
    let { showTapHint } = $props();
</script>

<div class="animate__animated animate__slideInDown animate__slow">
    <img src="/img/hbd1.png" class="img" alt="HBD">
</div>

{#if showTapHint}
    <p class="animate__animated animate__fadeIn animate__infinite animate__slow text-muted mt-5" style="cursor: pointer;">
        Ketuk layarnya ya...
    </p>
{/if}