<script>
  //this is the prop that you will pass where the component is declared
  export let show = false;
</script>

<!-- if show is true show the modal -->
{#if show}
  <div
    class="position-fixed top-50 start-50 d-flex justify-content-center align-items-center w-100 h-100 "
    style="transform: translate(-50%, -50%);background-color: rgba(0, 0, 0, 0.3);"
  >
    <div class="p-5 rounded text-center bg-dark" style="max-width: 400px;">
      <h5 class="text-dark text-white mb-4">Do you want to end the test?</h5>
      <div class="buttons  ">
        <button
          style="margin-right: 15px;"
          class="btn btn-danger"
          on:click|self={() => (show = false)}>NO</button
        >
        <a href="/result">
          <button class="btn btn-danger">YES</button>
        </a>
      </div>
    </div>
  </div>
{/if}
