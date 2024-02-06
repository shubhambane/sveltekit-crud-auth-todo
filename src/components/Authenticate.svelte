<script>

import { authHandlers } from "../store/store";


    let email = '';
    let password = '';
    let confirmPassword = '';
    let error = false;
    let register = false;
    let authenticating = false;
    async function handleAuthenticate() {
        if (authenticating) {
            return;
        }
        if (!email || !password || (register && !confirmPassword)) {
            error = true;
            return;
        }
        authenticating = true;

        try {
            if (!register) {
                await authHandlers.login(email, password);
            } else {
                await authHandlers.signup(email, password);
            }
        } catch (err) {
            console.log("There was an auth error", err);
            error = true;
            authenticating = false;
        }
    }

    function handleRegister() {
        register = !register;
    }


</script>

<div class="authContainer">
    <form action="">
        <h1>{register ? 'Register' : 'Login'}</h1>
        <label for="email">
            <input bind:value={email} type="email" placeholder="Email">
        </label>
        <label for="password">
            <input bind:value={password} type="password" placeholder="Password">
        </label>

        {#if register}

        <label for="confirmPassword">
            <input bind:value={confirmPassword} type="password" placeholder="Confirm Password">
        </label>
        {/if}

        {#if error}
        <p class="error">
            The information you entered is incorrect.
        </p>
        {/if}
       
        <button on:click={handleAuthenticate} type="submit" class="submitBtn">
            {#if authenticating}
            <i class="fa-solid fa-spinner loadingSpinner spin" />
        {:else}
            Submit
        {/if}
        </button>
    </form>
    <!-- <p>Register</p> -->
    {#if register}
    <button class="options" type="button" on:click={handleRegister}>Already have an account? <b>Login</b></button> 
    {:else}
    <button class="options" type="button" on:click={handleRegister}>Don't have an account? <b>Register</b></button>
    {/if}
</div>

<style>
    .authContainer {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        flex: 1;
        padding: 24px;
    }
    form {
        display: flex;
        flex-direction: column;
       gap: 16px;
       width: 400px;
       max-width: 100%;
       margin: 0 auto;
    }

    form label {
       position: relative;
       border: 1px solid #aaaaaa;
       border-radius: 8px;
    }

    form label:focus-within {
        border: 1px solid #000;
    }

    form input {
        width: 100%;
        border: none;
        background: transparent;
        color: #000;
        padding: 14px;
    }

    form input:focus {
        outline: none;
        border: none;
    }
    form button {
        border: none;
        background: #000;
        color: #fff;
        padding: 14px;
        border-radius: 8px;
        cursor: pointer;
        font-size: 1.1em;
        display: grid;
        place-content: center;
    }
    .spin {
        animation: spin 2s  infinite;
    }

    @keyframes spin {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }


    form button:hover {
        background: #222222;
    }

    h1 {
        text-align: center;
        font-size: 3em;
    }
    .options {
        border: none;
        background: transparent;
        color: #444444;
        padding: 14px;
        border-radius: 8px;
        cursor: pointer;
        font-size: 0.9em;
    }

    .error {
        color: red;
        font-size: 0.9em;
    }
    </style>