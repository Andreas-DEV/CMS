<script lang="ts">
  import Login from "./lib/Login.svelte";
  import { pb, currentUser } from "./lib/pocketbase";
  import Admin from "./lib/Admin.svelte";
</script>

{#if $currentUser}
  <Admin />
{:else}
  <Login />
{/if}
