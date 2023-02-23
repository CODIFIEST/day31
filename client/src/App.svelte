<script lang="ts">
  import Home from "./pages/Home.svelte";
  import Router from "svelte-spa-router";

  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import LoginPage from "./pages/LoginPage.svelte";
  import NotFound from "./pages/NotFound.svelte";
  import EditUser from "./pages/EditUser.svelte";
  import DisplayUsers from "./pages/DisplayUsers.svelte";
  import CreateUser from "./pages/CreateUser.svelte";
  import Notifications from "svelte-notifications";

  const routes = {
    // Exact path
    "/": Home,
    // route to create a user to be able to log in
    "/register": CreateUser,
    // Using named parameters, with last being optional
    "/login": LoginPage,

    // Display all users
    "/userlist": DisplayUsers,
    //edit only your own user
    "/edituser": EditUser,

    // Catch-all
    // This is optional, but if present it must be the last
    "*": NotFound,
  };
</script>

<main>
  <Header />
  <div
    class="hero min-h-screen"
    style="background-image: url('https://www.arweave.net/hNN-l4QsOuWIRWwpOn-VDjso2NsGBW3Mg30p18Gs6zQ?ext=png');"
  >
    <div class="hero-overlay bg-opacity-60" />
    <div class="hero-content text-center">
      <div class="max-w-3xl">
        <Notifications>
          <Router {routes} />
        </Notifications>
      </div>
    </div>
  </div>

  <Footer />
</main>

<!-- <style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style> -->
