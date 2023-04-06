<script>
  import { createEventDispatcher } from "svelte";
  import SidePanel from "./SidePanel.svelte";
  const dispatch = createEventDispatcher();
  export let question_no;
  let sidebar_show = false;
  let inReviewFooter = true;

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
    class="d-flex justify-content-evenly p-2 align-items-center bgColor text-white"
  >
    <button
      on:click={() => (sidebar_show = !sidebar_show)}
      class="btn btn-danger text-white"
    >
      List
    </button>
    <SidePanel
      bind:inReviewFooter
      bind:show={sidebar_show}
      on:displayQuesNum={displayQuesNum}
    />

    <a
      on:click={prevPage}
      href="/review?qno={parseInt(question_no)}"
      class="btn btn-primary"
      style={parseInt(question_no) <= 1 ? "pointer-events:none;" : ""}
      >Previous</a
    >
    <button class="btn text-white">
      {parseInt(question_no)} of 11
    </button>
    <a
      on:click={nextPage}
      href="/review?qno={parseInt(question_no)}"
      class="btn btn-primary"
      style={parseInt(question_no) > 10 ? "pointer-events:none;" : ""}>Next</a
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
