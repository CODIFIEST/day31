<script lang="ts">

    import { push } from "svelte-spa-router";
    import isLoggedIn from "../stores/isLoggedIn";
   
    async function logout() {
        document.cookie = null;
        isLoggedIn.set(false);
    }
</script>

{#if $isLoggedIn}
    <button
        on:click={async () => {
            await logout();
            await push('/')
            // // these next two lines reload the page
            // location.reload();
            // return false;
        }}
        class="btn">Log Out</button
    >
{:else}
    <button
        on:click={async () => {
          await push("/login");
        }}
        class="btn">

        Login</button>

{/if}
<!-- 
<style global lang="postcss">
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style> -->
