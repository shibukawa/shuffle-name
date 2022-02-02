<script lang="ts">

  import "./assets/app.css"

  let choices : string[] = [];

  function modifyValues(e: Event) {
    e.preventDefault();
    const ta = e.target as HTMLTextAreaElement;
    choices = ta.value.split("\n").filter(v => Boolean(v));
    shuffle();
  }

  function shuffle() {
    const orders = choices.map((v) => [v, Math.random()] as [string, number]);
    console.log(orders)
    orders.sort((a, b) => a[1] < b[1] ? -1 : 1);
    choices = orders.map(order => order[0]);
  }
</script>

<header class="navbar mb-2 shadow-lg bg-neutral text-neutral-content rounded-box">
  <div class="flex-1 px-2 mx-2">
    <span class="text-lg font-bold">
      勉強会発表順決定
    </span>
  </div> 
</header>

<main class="flex flex-col w-full grow lg:flex-row items-stretch">
  <div class="flex flex-grow h-full card rounded-box shadow-2xl p-6">
    <h2 class="grow-0 font-medium leading-tight text-4xl mt-0 mb-2 text-blue-600">参加者一覧(改行区切り)</h2>
    <textarea class="m-6 p-1 textarea textarea-bordered grow h-full" on:input={modifyValues}></textarea>
  </div> 
  <div class="divider lg:divider-vertical"></div> 
  <div class="flex flex-grow h-full card rounded-box shadow-2xl p-6">
    <h2 class="grow-0 font-medium leading-tight text-4xl mt-0 mb-2 text-blue-600">シャッフル結果</h2>
    <div class="grow">
      <ul>
        {#each choices as choice, i}
          <li class="rounded-lg p-2 m-2 border-emerald-400 bg-emerald-200 text-left">{i+1}: {choice}</li>
        {/each}
      </ul>
      </div>
    <button class="grow-0 btn" on:click={shuffle}>🎲再シャッフル</button>
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    height: 100%;
    width: 100%;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
</style>
