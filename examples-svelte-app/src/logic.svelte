<!--
Unlike HTML, Svelte allows for conditionals and loops.
- You can wrap markup in an `if` block as seen with the `Log out` and `Log in` buttons. You can also wrap markup in an
`if-else` block as seen with the `Sign in` and ` Sign out` buttons. Conditional statements can be chained as seen with
the `user.age` checks.
- You can use `each` blocks to iterate over lists of items. The first argument in the `each` block identifies the items
being iterated over and the second argument, which is optional, can be used to get the current index of the item. Look
at the `user.favColors` markup for an example.
-->
<script>
    let user = { loggedIn: false,
        signedIn:false,
        age: 0,
        favColors: [
            'Red',
            'Blue',
            'Purple'
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
{#each user.favColors as color, index}
    <p>{index + 1} - {color}</p>{/each}