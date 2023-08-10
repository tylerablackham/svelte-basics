<!--
- Props are properties declared that allow you to pass data from one component to its children.
- The prop, 'number', is not defined here but it is exported, and in the App.svelte file, it is defined when the Props
component is added. If you remove export from the declaration of 'number', you'll see that it becomes undefined.
- Props can be given a default value also, as seen with 'number2'. If a value is not specified in App.svelte, then it will
stick to the default value instead of being undefined.
-->


<script>
    export let number
    export let number2 = 'I forgot what numbers are...'
</script>

<p>Here's a fun number: {number}</p>
<p>Here's another fun number: {number2}</p>