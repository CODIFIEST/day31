<script lang="ts">
    import axios from "axios";
    import { onMount } from "svelte";
    import { push } from "svelte-spa-router";
    import type { UserC } from "../domain/user";
    import editUser from "../stores/editUser";
    import email from "../stores/email";
    import idToEdit from "../stores/id";
    import username from "../stores/username";

    let users: UserC[] = [];
    async function getUsers() {
        const result = await axios.get("https://day31-c.vercel.app/user");
        console.log("results", result.data);
        return result.data;
    }
    onMount(async () => {
        users = (await getUsers()) as any as UserC[];
        console.log("users", users);
    });
</script>

<div class="overflow-x-auto">
    <table class="table w-full">
        <!-- head -->
        <thead>
            <tr>
                <th />
                <th>Name</th>
                <th>Email</th>
            </tr>
        </thead>
        <tbody>
            {#each users as user}
                <!-- row 1 -->
                <tr
                    on:click={async () => {
                        idToEdit.set(user.id);
                        editUser.set(true);
                        username.set(user.username);
                        email.set(user.email);
                        console.log($idToEdit);
                        await push("/edituser");
                    }}
                    on:keypress={() => {
                        alert("nope");
                    }}
                    id={user.id}
                    class="hover"
                >
                    <th />
                    <td>{user.username}</td>
                    <td>{user.email}</td>
                </tr>
            {/each}
        </tbody>
    </table>
</div>
