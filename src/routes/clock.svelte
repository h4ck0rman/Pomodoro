<script>
    import {onMount, onDestroy} from 'svelte';
    let pomodoroTime = 25 * 60;
    let timeElapsed = 0;

    // Start and Stop the timer
    let running = false;
    let stateButton = 'start';
    const toggleState = () => {
        running = !running;
        stateButton = running ? 'pause' : 'start'
    } 

    // Reset the timer 
    const resetTimer = () => {
        timeElapsed = 0;
        running = false
        stateButton = 'start'
    }

    // Set up a counter that increments every second
    let interval = null;
    onMount(() => {
		interval = setInterval(() => {
            if (running) {
                timeElapsed += 1
            }
            
		}, 1000);
	});
    onDestroy(() => {
		clearInterval(interval);
	});

    // add prefix zeroes to single digit strings
    function numPadding (num) {
        let res = num.toString();
        while (res.length < 2) res = "0" + res
        return res
    }

    $: timeLeft = pomodoroTime - timeElapsed;
    $: minutes = numPadding(Math.floor(timeLeft / 60));
    $: seconds = numPadding(Math.floor(timeLeft % 60));
    

</script>


<div class="container mx-auto flex-col content-center py">
    <h1 class="text-white text-center text-9xl font-monaco 3font-semibold tracking-wide">{minutes}:{seconds}</h1>
    <div class="content-center flex justify-center py-5">
        <button on:click={toggleState} class="btn-timer" >{stateButton}</button>
        <button on:click={resetTimer}  class="btn-timer">reset</button>
    </div>
    
</div>
