<script>
  import { fly } from "svelte/transition";
  import { createEventDispatcher } from "svelte";
  import { questiondata_store, choosingans_store } from "../store/store.js";
  import { afterUpdate } from "svelte";
  const dispatch = createEventDispatcher();
  export let show = false;
  let total_attempted = 0;
  afterUpdate(() => {
    let data = $choosingans_store.filter(Boolean);
    total_attempted = data.length;
  });
  const displayQues = (i) => {
    dispatch("displayQuesNum", i);
  };
</script>

{#if show}
  <nav
    class="position-fixed  start-0  bgColor text-white d-flex flex-column p-2 pb-2"
    style="width:400px;top:58px;"
    transition:fly={{ x: -250, opacity: 1 }}
  >
    <p class="btn btn-success">Attempted questions : {total_attempted}</p>
    <p class="btn btn-warning">
      Unattempted Questions : {$questiondata_store.length - total_attempted}
    </p>
    {#each $questiondata_store as data, i}
      <span
        class="p-1"
        style="cursor: pointer;"
        on:click={() => displayQues(i)}
        on:click={() => (show = false)}
      >
        <span class="btn btn-primary btn-sm text-white fw-bold">{i + 1}. </span>
        <span> {data.snippet}</span>
        <!-- {#if $choosingans_store[i] == null}
          <span class="badge rounded-pill text-bg-warning">Unattempted</span>
        {:else}
          <span class="badge rounded-pill text-bg-success">Attempted</span>
        {/if} -->
      </span>
      <hr />
    {/each}
  </nav>
{/if}

<style>
  nav {
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    padding: 2rem 1rem 0.6rem;
    border-left: 1px solid #aaa;
    background: rgb(246, 244, 244);
    overflow-y: auto;
    width: 17rem;
    border-right: 1px solid black;
  }
  .bgColor {
    background-color: black;
  }
</style>
