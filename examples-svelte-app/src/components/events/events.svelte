<!--
- You can listen to any event on an element with the 'on:' directive
- You can also declare inline event handlers as seen on line 46
- Event handlers can have modifiers, as seen on line 50, a full list of modifiers can be found here: https://svelte.dev/tutorial/event-modifiers
- Components can dispatch events with an event dispatcher using 'createEventDispatcher'. The function 'tickled()' dispatches
an event. Which is then received in the 'App.svelte' file on line 33 where the event is then processed. The property
'tickled' and 'response' can both be changed to whatever you want.
- Component events don't bubble, meaning events in deeply nested components must be forwarded up. For example the
'Inner1' component that we import dispatches an event, but 'App.svelte' won't receive it unless it is also dispatched
in 'events.svelte'. Thankfully, there is some shorthand to do that. As seen on line 54 all we had to do was add the
'on:tickled2' event directive without a value.
- DOM event forwarding works very similarly. The element in 'inner-events-2.svelte' forwards the 'click' event which is
then received here in 'events.svelte'.
-->

<script>
    let m = { x: 0, y: 0 };

    function handleMousemove(event) {
        m.x = event.clientX;
        m.y = event.clientY;
    }

    let clicked = false
    function handleClick() {
        alert('You only get one click. Hope it was worth it.');
        clicked = true
    }

    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    function tickles() {
        dispatch('tickled', {
            response: 'That tickles, hehehe!'
        })
    }

    import Inner1 from './inner-events-1.svelte'
    import Inner2 from './inner-events-2.svelte'
</script>

<div on:mousemove={handleMousemove}>
    <p>The mouse position is {m.x} x {m.y}</p>
</div>

<div on:mousemove={(e) => (m = { x: e.clientX, y: e.clientY })}>
    <p>The mouse position is {m.x} x {m.y}</p>
</div>
<div>
    <button on:click|once={handleClick}> {clicked ? 'Already Clicked :/' : 'Click Me ;)'} </button>
    <button on:click={tickles}> You can click me infinitely </button>
</div>
<div>
    <Inner1 on:tickled2/>
    <Inner2 on:click={() => {alert('Stop... please')}}/>
</div>
