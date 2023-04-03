<script>
  import { createEventDispatcher } from "svelte";
  import SidePanel from "./SidePanel.svelte";
  const dispatch = createEventDispatcher();
  export let question_no;
  let sidebar_show = false;

  const prevPage = () => {
    dispatch("prevPage_rev");
  };

  const nextPage = () => {
    dispatch("nextPage_rev");
  };

  const displayQuesNum = (event) => {
    dispatch("updateQues_rev", parseInt(event.detail) + 1);
  };
</script>

<div>
  <div
    class="d-flex justify-content-between p-2 align-items-center bgColor  text-white"
  >
    <button
      on:click={() => (sidebar_show = !sidebar_show)}
      class="btn btn-danger"
    >
      List
    </button>
    <SidePanel bind:show={sidebar_show} on:displayQuesNum={displayQuesNum} />

    <button
      on:click={prevPage}
      class="btn btn-primary"
      disabled={parseInt(question_no) <= 1 ? true : false}>Previous</button
    >
    <button class="btn text-white">
      {parseInt(question_no)} of 11
    </button>
    <button
      on:click={nextPage}
      class="btn btn-primary"
      disabled={parseInt(question_no) > 10 ? true : false}>Next</button
    >
    <a class="" href="/">
      <button class="btn btn-primary">Dashboard</button>
    </a>
    <a class="" href="/result">
      <button class="btn btn-success">Result</button>
    </a>
  </div>
</div>

<style>
  .bgColor {
    background-color: black;
    /* opacity: 0.5; */
  }
</style>
