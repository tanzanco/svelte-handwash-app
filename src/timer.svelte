<script>
    import { createEventDispatcher } from 'svelte';
    import ProgressBar from './ProgressBar.svelte';
    const totalseconds = 20;
    let secondsLeft = totalseconds;
    let isRunning = false;
    $: progress = ((totalseconds - secondsLeft) / totalseconds) * 100;
    const dispatch = createEventDispatcher();
    function startTimer () {
        const timer = setInterval(() => {
            isRunning = true;
            secondsLeft -= 1;
            if (secondsLeft == 0) {
                clearInterval(timer);
                isRunning = false;
                secondsLeft = totalseconds;
                dispatch('end', "end timer");
            }
        }, 1000);
    };
    
</script>
<style>
    h2{
        margin: 0;
    }
    .start{
        background-color: rgb(154, 73, 73);
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled]{
        background-color: rgb(194, 194, 194);
        cursor: not-allowed;
    }
</style>
<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">
        Seconds Left: {secondsLeft}
    </h2>
    
</div>
<ProgressBar progress={progress}/>
<div bp="grid">
    <button disabled={isRunning} on:click={startTimer} bp="offset-5@md 4@md 12@sm" class="start">Start</button>
</div>
