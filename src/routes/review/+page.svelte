<script>
  import HeaderPart from "../../components/HeaderPart.svelte";
  import ReviewFooter from "../../components/ReviewFooter.svelte";
  import { onMount } from "svelte";
  let question_no;
  let all_questions = [];
  onMount(async () => {
    const response = await fetch("data/question.json");
    all_questions = await response.json();
    question_no = new URL(location.href).searchParams.get("qno");
  });
  // afterUpdate(() => {
  //   console.log("url updated");
  // });
</script>

<div class="mycontainer bgColor">
  <HeaderPart />
  <div class="container containerQues">
    {#each all_questions as data, i}
      {#if question_no - 1 === i}
        <div class="text-white">
          <span class="h4">
            {i + 1} . {JSON.parse(data.content_text).question}
          </span>
          <div
            class="d-flex text-white flex-column mt-4 text-primary font-weight-bold"
          >
            {#each JSON.parse(data.content_text).answers as answers, j}
              <div class="d-flex">
                {#if answers.is_correct == 1}
                  <p class="h6 my-auto">{String.fromCharCode(65 + j)}</p>
                  <label class="w-100 m-2 text-success">
                    <input type="radio" checked />
                    {@html answers.answer}
                  </label>
                {:else}
                  <p class="h6 my-auto">{String.fromCharCode(65 + j)}</p>
                  <label class="w-100 m-2">
                    <input type="radio" disabled />
                    {@html answers.answer}
                  </label>
                {/if}
              </div>
            {/each}
            <div class="mt-3 text-warning">
              {@html JSON.parse(all_questions[question_no - 1].content_text)
                .explanation}
            </div>
          </div>
        </div>
      {/if}
    {/each}
  </div>
</div>

<div
  class="position-fixed w-50  bg-dark text-white"
  style="bottom:15px;right:15px"
>
  <ReviewFooter
    {question_no}
    on:prevPage_rev={() => {
      question_no = parseInt(question_no) - 1;
      console.log("question_no : ", question_no);
    }}
    on:nextPage_rev={() => {
      question_no = parseInt(question_no) + 1;
      console.log("question_no : ", question_no);
    }}
    on:updateQues_rev={(event) => {
      question_no = event.detail;
    }}
  />
</div>

<style>
  body {
    color: white;
  }
  :global(seq::before) {
    content: attr(no);
    text-transform: uppercase;
  }

  .mycontainer {
    min-height: 100vh;
    min-width: 925px !important;
  }

  .containerQues {
    margin-top: 50px;
  }
  .bgColor {
    /* background: rgb(2, 0, 36);
    background: linear-gradient(
      180deg,
      rgba(0, 0, 0, 1) 0%,
      rgba(0, 0, 0, 1) 27%,
      rgba(0, 212, 255, 1) 100%
    ); */
    background-color: black;
  }
</style>
