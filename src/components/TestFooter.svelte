<script>
  import { createEventDispatcher } from "svelte";
  import Modal from "./Modal.svelte";
  import SidePanel from "./SidePanel.svelte";
  import Timer from "./Timer.svelte";
  const dispatch = createEventDispatcher();
  export let current_question;
  let sidebar_show = false;
  let confirm_show = false;

  const prevPage = () => {
    dispatch("prevPage");
  };

  const nextPage = () => {
    dispatch("nextPage");
  };

  const displayQuesNum = (event) => {
    dispatch("updateQues", event.detail);
  };
</script>

<div>
  <div
    class="d-flex justify-content-evenly p-2 align-items-center bgColor  text-white "
  >
    <button class="btn btn-danger">
      <Timer />
    </button>

    <button
      on:click={() => (sidebar_show = !sidebar_show)}
      class="btn btn-warning"
    >
      List
    </button>
    <SidePanel bind:show={sidebar_show} on:displayQuesNum={displayQuesNum} />

    <button
      on:click={prevPage}
      on:click={() => (sidebar_show = false)}
      class="btn btn-primary"
      disabled={current_question < 1 ? true : false}>Previous</button
    >
    <button class="btn text-white">
      {current_question + 1} of 11
    </button>
    <button
      on:click={nextPage}
      on:click={() => (sidebar_show = false)}
      class="btn btn-primary"
      disabled={current_question + 1 > 10 ? true : false}>Next</button
    >

    <button
      class="btn btn-danger"
      on:click={() => (confirm_show = !confirm_show)}>End Test</button
    >
  </div>
</div>
<Modal bind:show={confirm_show} />

<style>
  .bgColor {
    background-color: black;
    /* opacity: 0.5; */
  }
</style>
