<script lang="ts">
    import email from "../stores/email";
    import idToEdit from "../stores/id";
    import username from "../stores/username";
    import axios from "axios";
    import type { UserC } from "../domain/user";
    import editUser from "../stores/editUser";
    import { pop, push } from "svelte-spa-router";
    let name: string = "";
    let emailaddy: string = "";

    async function putUser() {
        const newUser: UserC = {
            id: $idToEdit,
            username: name,
            email: emailaddy,
        };
        const result = await axios
            .put("https://day29-neon.vercel.app/user/:id", newUser, {
                // withCredentials: true,
                headers: { Authorization: `Bearer ${document.cookie}` },
            })
            .then((res) => {
                // alert(res.statusText)
            })
            .catch((error) => {
                alert(error);
            })
            .finally(() => {
                editUser.set(false);
                return result.data;
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
                        alert(`${username} ${email} updated`);
                        await push("/userlist");
                    }}
                    class="btn">Submit changes</button
                >
                <br /><br />
                <button
                    on:click={async () => {
                        alert("changes not saved");
                        await pop();
                    }}
                    class="btn">Cancel</button
                >
            </div>
        </div>
    </div>
</main>
