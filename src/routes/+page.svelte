<script>
    import { onMount } from 'svelte';
    import CountDown from "$lib/+countDown.svelte";
    import SlideSatu from "$lib/+slideSatu.svelte";
    import SlideDua from "$lib/+slideDua.svelte";
    import SlideTiga from "$lib/+slideTiga.svelte";
    import SlideEmpat from "$lib/+slideEmpat.svelte";
    import SlideLima from "$lib/+slideLima.svelte";
    import Footer from "$lib/+footer.svelte";
    import audio from "$lib/assets/music/monokrom.mp3";

    let currentSlide = $state(0); 
    let showTapHint = $state(false);
    let isMusicPlaying = false; 

    // Tentukan tanggal ulang tahun di satu tempat agar terpusat
    const TARGET_DATE = new Date('May 25, 2026 00:00:00').getTime();

    function playMusic() {
        if (isMusicPlaying) return; 
        
        const music = document.getElementById('background-music');
        if (music) {
            music.play().then(() => {
                isMusicPlaying = true;
            }).catch(e => {
                console.log("Autoplay dihambat peramban, menunggu ketukan murni pengguna.");
            });
        }
    }

    function aktifkanAudioMurni() {
        playMusic();
    }

    onMount(() => {
        if (Date.now() >= TARGET_DATE) {
            currentSlide = 1;
            showTapHint = true; 
            
            document.body.addEventListener('click', aktifkanAudioMurni, { once: true });
        }

        return () => {
            document.body.removeEventListener('click', aktifkanAudioMurni);
        };
    });

    function tanganiTimerSelesai() {
        currentSlide = 1;
        playMusic(); // Coba jalankan otomatis
        
        document.body.addEventListener('click', aktifkanAudioMurni, { once: true });
        
        setTimeout(() => { 
            showTapHint = true; 
        }, 3500);
    }

    function tanganiKlikLayar() {
        if (currentSlide > 0) {
            playMusic();
        }

        if (!showTapHint) return;
        showTapHint = false; 

        if (currentSlide === 1) {
            currentSlide = 2;
        } else if (currentSlide === 2) {
            currentSlide = 3;
        } else if (currentSlide === 3) {
            currentSlide = 4;
        }
    }
</script>

<audio id="background-music" src={audio} preload="auto"></audio>

<div class="bg" onclick={tanganiKlikLayar}>
    {#if currentSlide === 0}
        <CountDown {TARGET_DATE} onTimerEnd={tanganiTimerSelesai} />
    {/if}

    {#if currentSlide === 1}
        <SlideSatu {showTapHint} />
    {/if}

    {#if currentSlide === 2}
        <SlideDua {showTapHint} onComplete={() => showTapHint = true} />
    {/if}

    {#if currentSlide === 3}
        <SlideTiga {showTapHint} onComplete={() => showTapHint = true} />
    {/if}

    {#if currentSlide === 4}
        <SlideEmpat onSuka={() => { currentSlide = 5; }} />
    {/if}

    {#if currentSlide === 5}
        <SlideLima />
    {/if}
    <Footer />
</div>