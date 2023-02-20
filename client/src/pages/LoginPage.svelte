<script lang="ts">
    
    import { push } from "svelte-spa-router";
    import isLoggedIn from "../stores/isLoggedIn";
    
    import axios from "axios";
    let email: string = "";
    let password: string = "";

    async function submitForm() {
        console.log(email, password);
        if (password && email) {
            const result = await axios
                .post("https://day29-neon.vercel.app/login", {
                    email: email,
                    password: password,
                })
                .then(async (res) => {
                    document.cookie = res.data.token;
                    alert("login successful");
                    console.log("result.data", res.data);
                    isLoggedIn.set(true);
                    await push("/userlist");
                })
                .catch(async(error) => {
                    await push("/");
                    alert(error);
                })
                .finally(() => {});
            // get token from fetch request
        }
    }

</script>
<div class="card w-96 bg-base-100 shadow-xl">
    <div class="card-body">
        <div style="float: right;">
            email:
            <input
                bind:value={email}
                class="input input-bordered input-primary w-full max-w-xs"
                type="text"
            />
            <br />
            password:
            <input
                bind:value={password}
                class="input input-bordered input-primary w-full max-w-xs"
                type="text"
            />
        </div>
        
      <div class="card-actions justify-end">
        <button
        on:click={async () => {
            console.log("button clicked");
            if (password && email) {
                await submitForm();

                // these next two lines reload the page
                // location.reload();
                // return false;
               
            }
        }}
        class="btn">Submit</button
    >
      </div>
    </div>
  </div>
        
