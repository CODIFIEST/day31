<script lang="ts">
    import { pop, push } from "svelte-spa-router";
    import isLoggedIn from "../stores/isLoggedIn";
    import axios from "axios";
    import { getNotificationsContext } from "svelte-notifications";

    const { addNotification } = getNotificationsContext();

    function loginSuccess() {
        addNotification({
            text:'Login successful',
            position:"bottom-center",
            type: 'success',
            removeAfter: 4000,
        })
    }
    function loginFail(){
        addNotification({
            text:'Incorrect email or password, try agian.',
            position:'bottom-center',
            type:'error',
            removeAfter:4000,
        })
    }

    let email: string = "";
    let password: string = "";

    async function submitForm() {
        console.log(email, password);
        if (password && email) {
            const result = await axios
                .post("https://day31-tan.vercel.app/login", {
                    email: email,
                    password: password,
                })
                .then(async (res) => {
                    document.cookie = res.data.token;
                    // alert("login successful");
                    //instead of alert, send green text to screen or modal
                    loginSuccess();
                    console.log("result.data", res.data);
                    isLoggedIn.set(true);
                    await push("/userlist");
                })
                .catch(async (error) => {
                    loginFail();
                    // await push("/login");
                    // await pop();
                    // alert("Incorrect email or password");
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
                    }
                }}
                class="btn">Submit</button
            >
        </div>
    </div>
</div>
