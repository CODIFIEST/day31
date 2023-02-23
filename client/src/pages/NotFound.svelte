<script lang="ts">
    import { onMount } from "svelte";
  import { push } from "svelte-spa-router";
 async function goHome(){
  setTimeout(async () => {
   await push("/");
  }, 5000);
  }
  onMount(async()=>{
    await goHome();
  })

</script>
<div class="card w-96 bg-base-100 shadow-xl">
  <div class="card-body">
    <h1 class="card-title">404</h1>
    <p>That page is not found... redirecting to home page.</p>
  
    <div class="card-actions justify-end">
      <!-- <button class="btn btn-primary">Buy Now</button> -->
    </div>
  </div>
</div>


