<!--
- You can bind values to component props, as seen in Example 1.
- You can also bind the entire component instance itself, as seen in Example 2, in a similar way.
-->
<script>
    import Keypad from './Keypad.svelte';
    let pin;
    $: view = pin ? pin.replace(/\d(?!$)/g, '•') : 'enter your pin';
    function handleSubmit() {
        alert(`submitted ${pin}`);
    }

    import InputField from './InputField.svelte'
    let field
</script>
<!--Example 1-->
<h1 style="color: {pin ? '#000' : '#ccc'}">{view}</h1>
<div style="display: flex; justify-content: center; justify-content: space-evenly">
    <Keypad bind:value={pin} on:submit={handleSubmit}/>
</div>

<!--Example 2-->
<div style="padding: 2em">
    <InputField bind:this={field} />
    <button on:click={field.focus}> Focus field </button>
</div>
