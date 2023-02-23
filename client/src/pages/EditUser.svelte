<script lang="ts">
    import email from "../stores/email";
    import idToEdit from "../stores/id";
    import username from "../stores/username";
    import axios from "axios";
    import type { UserC } from "../domain/user";
    import editUser from "../stores/editUser";
    import { pop, push } from "svelte-spa-router";
    import { getNotificationsContext } from "svelte-notifications";

    const { addNotification } = getNotificationsContext();

    function editSuccess() {
        addNotification({
            text: `${$username} ${$email} updated`,
            position: "bottom-center",
            type: "success",
            removeAfter: 4000,
        });
    }
    function editFail() {
        addNotification({
            text: "You can only edit your user.",
            position: "bottom-center",
            type: "error",
            removeAfter: 4000,
        });
    }

    function NothingHappened() {
        addNotification({
            text: "No changes were made",
            position: "bottom-center",
           
            removeAfter: 4000,
        });
    }

    let name: string = "";
    let emailaddy: string = "";

    async function putUser() {
        const newUser: UserC = {
            id: $idToEdit,
            username: name,
            email: emailaddy,
        };
        const result = await axios
            .put("https://day31-tan.vercel.app/user/:id", newUser, {
                // withCredentials: true,
                headers: { Authorization: `Bearer ${document.cookie}` },
            })
            .then(async (res) => {
                // return res.data;
                // alert(`${$username} ${$email} updated`);
                editSuccess();
                await push("/userlist");
            })
            .catch((error) => {
                // alert("You can only edit your user.");
                editFail();
            })
            .finally(() => {
                // editUser.set(false);
                // return result.data
            });
    }
</script>

<main>
    <div class="card w-96 bg-base-100 shadow-xl">
        <div class="card-body">
            <div style="float:right">
                name: {$username} <br />

                <input
                    class="input input-bordered input-primary w-full max-w-xs"
                    bind:value={name}
                    type="text"
                    placeholder={$username}
                />
                <br />
                email: {$email}
                <input
                    class="input input-bordered input-primary w-full max-w-xs"
                    bind:value={emailaddy}
                    type="text"
                    placeholder={$email}
                />
            </div>

            <div class="card-actions justify-end">
                <button
                    on:click={async () => {
                        await putUser();


                    }}
                    class="btn">Submit changes</button
                >
                <br /><br />
                <button
                    on:click={async () => {    
                        await pop();
                        NothingHappened();
                    }}
                    class="btn">Cancel</button
                >
            </div>
        </div>
    </div>
</main>
