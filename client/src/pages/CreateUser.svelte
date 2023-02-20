<script lang="ts">
    // import email from "../stores/email";
    // import username from "../stores/username";
    import axios from "axios";
    import { pop, push } from "svelte-spa-router";
    import isLoggedIn from "../stores/isLoggedIn";
    let username: string = "";
    let email: string = "";
    let password: string = "";

    async function submitForm() {
        console.log(email, username, password);
        if (username && email) {
            const result = await axios.post(
                "https://day31-tan.vercel.app/user",
                {
                    email: email,
                    username: username,
                    password: password,
                },
                {
                    withCredentials: false,
                    // headers: // TODO: add authentication to header on login, maybe not here on creation
                    // {'Access-Control-Allow-Origin': '*'}
                }
            )
            .then((res)=>{

                alert("User created successfully");
            })
            .catch((error) => {
                alert('That email already exists. Use another.');
            })

            
        }
    }
</script>

<div class="card w-96 bg-base-100 shadow-xl">
    <div class="card-body">
        <div>
            username: <input
                bind:value={username}
                class="input input-bordered input-primary w-full max-w-xs"
                type="text"
            />
        </div>
        <div>
            email:
            <input
                bind:value={email}
                class="input input-bordered input-primary w-full max-w-xs"
                type="text"
            />
        </div>
        <div>
            password:
            <input
                bind:value={password}
                class="input input-bordered input-primary w-full max-w-xs"
                type="text"
            />
        </div>
        <div>
            <button
                on:click={async () => {
                    
                  await pop();
                  alert('No changes made')
                }}
                class="btn">Cancel</button
            >
        </div>
        <div class="card-actions justify-end">
            <button
                on:click={async () => {
                    console.log("button clicked");
                    if (username && email) {
                        await submitForm();
                    
                        await push("/userlist")
                       
                    }
                }}
                class="btn">Submit</button
            >
        </div>
    </div>
</div>
