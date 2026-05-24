<script>
    import { onMount } from 'svelte';
    import confetti from 'canvas-confetti';

    // Menerima fungsi callback dari parent menggunakan rune $props
    let { TARGET_DATE, onTimerEnd } = $props();

    let days = $state(0);
    let hours = $state(0);
    let minutes = $state(0);
    let seconds = $state(0);
    let timerInterval;

    onMount(() => {
        //const countDownDate = Date.now();
        const countDownDate = TARGET_DATE; 
        
        timerInterval = setInterval(() => {
            const distance = countDownDate - Date.now();

            if (distance < 0) {
                clearInterval(timerInterval);
                confetti({ particleCount: 300, spread: 100, origin: { y: 0.6 } });
                onTimerEnd(); // Panggil fungsi dari parent
            } else {
                seconds = Math.floor((distance % (1000 * 60)) / 1000);
                minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
                hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                days = Math.floor(distance / (1000 * 60 * 60 * 24));
            }
        }, 1000);

        return () => clearInterval(timerInterval);
    });
</script>

<div class="container" id="timer">
    <h5>Countdown to birthday :</h5>
    <ul>
        <li><span>{days}</span>Days</li>
        <li><span>{hours}</span>Hours</li>
        <li><span>{minutes}</span>Minutes</li>
        <li><span>{seconds}</span>Seconds</li>
    </ul>
</div>