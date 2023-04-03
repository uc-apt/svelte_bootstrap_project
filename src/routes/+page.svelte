<script>
  import HeaderPart from "../components/HeaderPart.svelte";
</script>

<HeaderPart />
<div
  class=" d-flex min-vh-100 justify-content-center align-items-center mycontainer bgColor"
>
  <a href="/testpage">
    <button class="btn btn-primary">Start Test</button>
  </a>
</div>

<style>
  .mycontainer {
    min-width: 560px !important;
  }
  .bgColor {
    background: rgb(2, 0, 36);
    background: linear-gradient(
      180deg,
      rgba(0, 0, 0, 1) 0%,
      rgba(0, 0, 0, 1) 27%,
      rgba(0, 212, 255, 1) 100%
    );
  }
</style>
