<!--Here we look at reactivity, here are some examples:
 - count, which reacts to a button click
 - big, which reruns its declaration when any value referenced is changed
 - the console.log statement on line 10 is reactive statement
 - numbersOnReset is an array. the reactivity of arrays and objects work a
    little bit differently. if an array is only mutated, that change will not trigger
    and update. You can trigger an update by reassigning the array or object as seen on line 21 -->

<script>
    let count = 0;
    $: big = factorial(count)
    let countIsZero = true
    $: console.log(countIsZero ? 'Count set to zero' : 'Count is no longer zero')
    let numbersOnReset = []

    function incrementCount() {
        countIsZero = false
        count ++;
    }
    function reset() {
        countIsZero = true
        numbersOnReset = [...numbersOnReset, count]
        count = 0;
    }
    function factorial(num) {
        if (num <= 1) {return 1}
        return num * factorial(num-1)
    }
</script>

<button on:click={incrementCount}>
    Clicked {count}
    {count === 1 ? 'time' : 'times'}
</button>
<button on:click={reset}>
    Reset
</button>
<p> The factorial of {count} is {big} </p>
<p> Here's a list of the numbers that count was equal to each time you reset </p>
<p> [ {numbersOnReset.join(', ')} ] </p>

<style>
    button {
        width:200px;
    }
</style>