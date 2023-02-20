<script lang="ts">
  import { push } from "svelte-spa-router";
  import LoginButton from "./LoginButton.svelte";
</script>

<div class="navbar bg-base-100">
  <div class="flex-1">
    <button on:click={async () => await push("/")} class="btn">Home</button>
  </div>
  <div class="flex-none gap-2">
    <LoginButton />

    <button
      on:click={async () => {
        await push("/register");
      }}
      class="btn "
    >
      Register a new User
    </button>
  </div>
</div>
