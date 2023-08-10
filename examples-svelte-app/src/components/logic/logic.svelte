<!--
Unlike HTML, Svelte allows for conditionals and loops.
- You can wrap markup in an `if` block as seen with the `Log out` and `Log in` buttons. You can also wrap markup in an
`if-else` block as seen with the `Sign in` and ` Sign out` buttons. Conditional statements can be chained as seen with
the `user.age` checks.
- You can use `each` blocks to iterate over lists of items. The first argument in the `each` block identifies the items
being iterated over and the second argument, which is optional, can be used to get the current index of the item. Look
at the `user.favColors` markup for an example. There may be specific times when removing or adding an object like
`favColors` may not work as you intend. That is because Svelte by default add/removes items at the end of the block. If
that is happening you can specify a unique identify, or key, for the each block, as seen with the `(color.hex)`
statement.
- You can use `await` blocks to deal with asynchronous data. You can omit the first block if you don't want to show
anything until the promise resolves. You can also omit the catch block if you know that your promise won't reject
-->
<script>
    let user = { loggedIn: false,
        signedIn:false,
        age: 0,
        favColors: [
            {color: 'Red', hex: 'e30e0e'},
            {color: 'Blue', hex: '0e35e3'},
            {color: 'Purple', hex: 'a90ee3'}
        ]
    };

    function logIn() {
        user.loggedIn = !user.loggedIn;
    }
    function signIn() {
        user.signedIn = !user.signedIn;
    }
    function increase() {user.age = user.age + 1}
    function decrease() {user.age = user.age > 0 ? user.age - 1 : 0}
    function removeColor() {user.favColors = user.favColors.splice(1)}

    async function getRandomNumber() {
        const res = await fetch(`https://svelte.dev/tutorial/random-number`);
        const text = await res.text();

        if (res.ok) {
            return text;
        } else {
            throw new Error(text);
        }
    }

    let promise = getRandomNumber();

    function handleClick() {
        promise = getRandomNumber();
    }
</script>

{#if user.loggedIn}<button on:click={logIn}> Log out </button>{/if}
{#if !user.loggedIn}<button on:click={logIn}> Log in </button>{/if}

{#if user.signedIn}<button on:click={signIn}> Sign in </button>
    {:else}<button on:click={signIn}> Sign out </button>{/if}

<p>User is {user.age} years old.</p>
<div>
    <button on:click={decrease}>-</button>
    <button on:click={increase}>+</button>
</div>
{#if user.age < 8}<p>User is younger than 8</p>
    {:else if user.age < 12}<p>User is younger than 12</p>
    {:else if user.age < 18}<p>User is younger than 18</p>
    {:else}<p>User is older than 18</p>{/if}

<h4>User's Favorite Colors</h4>
{#each user.favColors as color, index (color.hex)}
    <p style="color: {color.color}">{index + 1} - {color.color}: #{color.hex}</p>{/each}
<button on:click={removeColor}>Remove first color</button>

<div>
    <button on:click={handleClick}> Generate Random Number </button>
    {#await promise}
        <p>...waiting</p>
    {:then number}
        <p>The number is {number}</p>
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}
</div>
