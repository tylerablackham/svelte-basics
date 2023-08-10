<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    function sayHello() {
        dispatch('tickled2', {
            laugh: 'Ha Ha Ha'
        });
    }
</script>

<button on:click={sayHello}> Don't forget me! </button>