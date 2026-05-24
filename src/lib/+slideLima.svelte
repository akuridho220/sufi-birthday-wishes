<script>
    import { onMount } from 'svelte';
    import TypeIt from 'typeit';

    let showTerimakasih = $state(false);

    const hearts1 = [25, 22, 20, 13, 16, 14, 26, 17, 10, 24, 18, 11, 19, 23, 21, 12];
    const hearts2 = [11, 20, 14, 16, 22, 26, 21, 17, 10, 18, 23, 19, 24, 13, 12, 25];

    onMount(() => {
        setTimeout(() => {
            showTerimakasih = true;
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

<div class="hujan-love-container">
    <div class="love-row">
        {#each hearts1 as i}
            <span class="heart" style="--i:{i}"></span>
        {/each}
    </div>
    <div class="love-row">
        {#each hearts2 as i}
            <span class="heart" style="--i:{i}"></span>
        {/each}
    </div>
</div>

<div class="container text-center" style="position: relative; top: 250px; z-index: 10;">
    <div class="animate__bounceIn animate__animated animate__slow">
        <i class="fas fa-heart fa-5x text-danger"></i>
    </div>
    {#if showTerimakasih}
        <p id="trims" class="text-muted mt-4" style="font-size: 1.5rem; position: relative; top: 0;"></p>
    {/if}
</div>

<style>
    /* Mengunci area hujan agar tidak membuat layar bisa di-scroll ke samping */
    .hujan-love-container {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        overflow: hidden;
        pointer-events: none; /* Penting! Agar hujan ini tidak menghalangi tombol atau klik layar */
        display: flex;
        justify-content: space-around;
        z-index: 0;
    }

    .love-row {
        display: flex;
        position: relative;
    }

    .heart {
        position: relative;
        top: -60vh;
        display: flex;
        margin: 0 15px; /* Sedikit dikecilkan agar muat banyak di layar hp */
        animation: rainy 10s linear infinite;
        animation-duration: calc(45s / var(--i));
    }

    /* Membentuk icon Love dari kode aslimu */
    .heart:before,
    .heart:after {
        content: "";
        background-color: #f70424; /* color-red-solid */
        position: absolute;
        height: 20px;
        width: 35px;
        border-radius: 15px 0px 0px 15px;
    }

    .heart:before {
        transform: rotate(45deg);
    }

    .heart:after {
        left: 10.5px;
        transform: rotate(135deg);
    }

    @keyframes rainy {
        0% {
            transform: translateY(-60vh) scale(1);
        }
        70% {
            transform: translateY(100vh) scale(1);
        }
        100% {
            transform: translateY(100vh) scale(0);
        }
    }
</style>