<script>
  export let question;
  export let answer = '';
  export let submit = () => {};
</script>

<main>
  <div class="flex flex-col items-center justify-center">
    <div class="w-full font-bold text-xl border-b pb-4 mb-4 text-center">{question}</div>
    <div class="md:w-1/2 w-full flex flex-col items-center justify-center">
      <input class="w-full mb-4 p-1 bg-gray-50 border focus:outline-none focus:border-indigo-400" bind:value={answer} />
      <button class="py-2 px-8 bg-indigo-500 text-white font-bold rounded" on:click={submit}>Submit</button>
    </div>
  </div>
</main>
