<script lang="ts">
    // import email from "../stores/email";
    // import username from "../stores/username";
    import axios from "axios";
    import { pop, push } from "svelte-spa-router";
    import isLoggedIn from "../stores/isLoggedIn";
    import { getNotificationsContext } from "svelte-notifications";

    const { addNotification } = getNotificationsContext();

    function createSuccess() {
        addNotification({
            text: "User created successfully. Log in to edit your user.",
            position: "bottom-center",
            type: "success",
            removeAfter: 4000,
        });
    }
    function createFail() {
        addNotification({
            text: "That email already exists. Use another.",
            position: "bottom-center",
            type: "error",
            removeAfter: 4000,
        });
    }

    function NothingHappened(){
        addNotification({
            text:'No changes were made',
            position:'bottom-center',
            removeAfter:4000,
        })
    }

    let username: string = "";
    let email: string = "";
    let password: string = "";

    async function submitForm() {
        console.log(email, username, password);
        if (username && email) {
            const result = await axios
                .post(
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
                .then(async (res) => {
                    // alert(
                    //     "User created successfully. Log in to edit your user."
                    // );
                    createSuccess();
                    await push("/login");
                })
                .catch((error) => {
                    createFail();
                    // alert("That email already exists. Use another.");
                });
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
                    NothingHappened();
                    // alert("No changes made");
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
                    }
                }}
                class="btn">Submit</button
            >
        </div>
    </div>
</div>
