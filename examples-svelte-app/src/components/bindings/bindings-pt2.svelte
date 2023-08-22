<!--
- You can add the 'multiple' attribute to a select to populate an rather than a sing value as seen in Example 1. To
select multiple on the page, hold the control key while clicking.
- Elements with the 'contenteditable' attribute, as seen in Example 2, can support the following bindings:
'innerHTML', 'innerText', 'textContent'. You can learn more about those bindings here:
https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent#Differences_from_innerText
- As seen in example 3, you can bind to properties inside an each block. This will allow the array to be mutated.
- <audio> and <video> elements also have properties you can bind to. I'm to lazy to demonstrate this here but you can
learn more about those bindings here: https://svelte.dev/tutorial/media-elements
- block-level elements have 'clientWidth', 'clientHeight', 'offsetWidth', and offsetHeight' bindings. They are readonly,
though which means changing the values bound to them won't do anything. Notice how, in example 4, changing the values of
'h' and 'w' with the sliders, does not effect the <div> that has those values bound to it.
-->
<script>
    let fruits = ['apple','mango','pineapple','banana','grape']
    let favFruits = []

    let html = '<p>Write some text!</p>';

    let otherFruits = [{name: 'kiwi', eaten: false},
        {name: 'star fruit', eaten: false},
        {name: 'tomato', eaten: false},
        {name: 'passion fruit', eaten: false}]
    function addOtherFruits() {otherFruits = otherFruits.concat({name: '', eaten: false})}
    function eat() {otherFruits = otherFruits.filter((fruit) => !fruit.eaten)}

    let w = 30
    let h = 10
    let size = 42
    let text = 'resize me'
</script>

<!--Example 1-->
<h4> Pick your favorite fruits </h4>
<select multiple bind:value={favFruits}>
    {#each fruits as fruit}
        <option value={fruit}>
            {fruit}
        </option>
    {/each}
</select>
<p> Here's a list of your favorite fruits: {favFruits.join(', ')}</p>

<!--Example 2-->
<div style="border: 1px solid #eee" contenteditable="true" bind:innerHTML={html}/>
<pre>{html}</pre>

<!--Example 3-->
{#each otherFruits as otherFruit}
    <div>
        <input type="checkbox" bind:checked={otherFruit.eaten}/>
        <input bind:value={otherFruit.name}/>
    </div>
{/each}
<button on:click={addOtherFruits}> Add Other Fruits </button>
<button on:click={eat}> Clear Eaten </button>

<!--Example 4-->
<div>
    <input type="range" bind:value={w} />
    <input type="range" bind:value={h} />
</div>
<div bind:clientWidth={w} bind:clientHeight={h}>
    <span>{text} ( hint: you can't :) )</span>
</div>
<input type="range" bind:value={size} />
<div>
    <span style="font-size: {size}px">{text}</span>
</div>
