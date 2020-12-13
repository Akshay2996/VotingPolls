<script>
  import { scale, fade } from "svelte/transition";
  import { flip } from "svelte/animate";
  import PollDetails from "./PollDetails.svelte";
  import PollStore from "../stores/PollStore.js";
  import { onDestroy } from "svelte";

  export let polls = [];

  const unsub = PollStore.subscribe((data) => {
    polls = data;
  });

  //  Lifecycle Hooks
  onDestroy(() => {
    // Unsubcribe from the store
    unsub();
  });
</script>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>

<div class="poll-list">
  {#each polls as poll (poll.id)}
    <div in:fade out:scale|local animate:flip={{duration : 500}}>
      <PollDetails {poll} />
    </div>
  {/each}
</div>
