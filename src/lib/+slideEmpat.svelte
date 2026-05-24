<script>
    let { onSuka } = $props();

    let btnTop = $state(0);
    let btnLeft = $state(0);

    function kabur() {
        btnTop = Math.floor(Math.random() * 80) - 40; 
        btnLeft = Math.floor(Math.random() * 80) - 40;
    }
</script>

<div class="kotak slides animate__animated animate__fadeInDown" onclick={(e) => e.stopPropagation()}>
    <div class="row">
        <div class="col-sm mt-1">
            <h5>Kamu suka nggak?</h5>
        </div>
    </div>
    <div class="row mt-2">
        <div class="col-4 offset-2">
            <button 
                onmouseover={kabur} 
                onclick={kabur}
                class="btn btn-outline-danger"
                style="transform: translate({btnLeft}px, {btnTop}px); transition: all 0.2s ease;"
            > 
                Gak! 
            </button>
        </div>
        <div class="col-4">
            <button onclick={onSuka} class="btn btn-outline-info"> 
                Suka!! 
            </button>
        </div>
    </div>
</div>