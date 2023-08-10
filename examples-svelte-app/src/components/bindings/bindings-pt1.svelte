<!--
- Data flow is top down. A parent component can set props ona child component but not the other way around. We can get
around that by using binding. All we have to do is use the 'bind:value' directive as seen with Example 1.
- The 'bind:value' directive takes care of numeric inputs for you, so that you don't have to use 'input.value' before
using that input, as seen with Example 2.
- Checkboxes work in a similar way, but we use 'bind:checked' rather than 'bind:value', as seen in Example 3.
- You can use the 'bind:group' directive in addition to the value attribute if you have multiple inputs that affect the
same value, as seen in Example 4. Radio inputs are mutually exclusive while checkbox inputs form an array of values
- If the name of your variable matches, leading to this 'bind:value={value}, you can use this shorthand 'bind:value',
as seen with Example 5
-->

<script>
    let name = 'world';

    let a = 1;
    let b = 2;

    let allergic = false

    let genders = ['male','female','other']
    let gender = ''
    let emotions = ['happy', 'sad', 'angry', 'bored']
    let emotion = []

    let value = ''
</script>

<!--Example 1-->
<input bind:value={name} />
<h1>Hello {name}!</h1>

<!--Example 2-->
<label style="display: flex; justify-content: center; justify-content: space-evenly">
    <input type="number" bind:value={a} min="0" max="10" />
    <input type="range" bind:value={a} min="0" max="10" />
</label>
<label style="display: flex; justify-content: center; justify-content: space-evenly">
    <input type="number" bind:value={b} min="0" max="10" />
    <input type="range" bind:value={b} min="0" max="10" />
</label>
<p>{a} + {b} = {a + b}</p>

<!--Example 3-->
<label>
    <input type="checkbox" bind:checked={allergic} />
    Check if you're allergic to peanuts
</label>
{#if allergic}<p>Dang that sucks. Sorry mate.</p>
    {:else}<p>Lucky you</p>{/if}
<button disabled={allergic}> Eat Peanut </button>
<button disabled={!allergic}> Refrain From Eating Peanut </button>

<!--Example 4-->
<h4>Pick a gender</h4>
<div style="display: flex; justify-content: center; justify-content: space-evenly">
    {#each genders as g}
        <label>
            <input type="radio" bind:group={gender} value={g}/>
            {g}
        </label>
    {/each}
</div>
<h4>Pick your emotions</h4>
<div style="display: flex; justify-content: center; justify-content: space-evenly">
    {#each emotions as e}
        <label>
            <input type="checkbox" bind:group={emotion} value={e}/>
            {e}
        </label>
    {/each}
</div>
<h4>That is one {emotion.length === 1 ? emotion[0]: emotion.join(', ')} {gender}</h4>

<!--Example 5-->
<p>This is what you typed: {value}</p>
<textarea bind:value/>
