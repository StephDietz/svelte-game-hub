<script>
  import RiddleCard from '../Components/RiddleCard.svelte';

  let question = 'What is the best JavaSript framework?';
  let frameworks = [
    {name: 'Vue', votes: 0, color: 'green-400'},
    {name: 'React', votes: 0, color: 'blue-400'},
    {name: 'Angular', votes: 0, color: 'red-600'},
    {name: 'Other', votes: 0, color: 'gray-400'}
  ];
  let riddle = {question: 'What question can you never answer yes to?', answer: 'Are you asleep yet?'}
  let riddleAnswer = '';
  let answeredCorrect = undefined;
  let triviaQuestions = [
    {
      question: 'Who is Snoop Dogg’s best celebrity friend?',
      answer: 2,
      options: [
        {option: 'Kevin Hart' , id: 1},
        {option: 'Martha Stewart' , id: 2},
        {option: 'Pete Davidson' , id: 3},
        {option: 'Travis Scott' , id: 4}
      ],
      id: 1
    },
    {
      question: 'Where did the singer Britney Spears get her start?',
      answer: 4,
      options: [
        {option: 'Disney Channel' , id: 1},
        {option: 'Modeling' , id: 2},
        {option: 'MTV' , id: 3},
        {option: 'The Mickey Mouse Club' , id: 4}
      ],
      id: 2
    },
    {
      question: 'What female rapper has six certified-platinum albums?',
      answer: 4,
      options: [
        {option: 'Nicki Minaj' , id: 1},
        {option: 'Lizzo' , id: 2},
        {option: 'Cardi B' , id: 3},
        {option: 'Missy Elliot' , id: 4}
      ],
      id: 3
    },
  ];
  let triviaAnswers = [2, 4, 4];
  let triviaResponses = [];
  let triviaQuestionNumber = 0;
  let finished = false;

  $: totalVotes = frameworks.reduce((sum, current) => {
    return sum + current.votes
  }, 0);

  const addVote = (name) => {
    frameworks = frameworks.map((framework) => {
      if(name === framework.name) {
        framework.votes ++
        return framework
      } else {
        return framework
      }
    })
  };

  const selectOption = (answer, id) => {
    if(answer === id) {
      triviaResponses.push(id);
      triviaResponses = triviaResponses;
    } else {
      triviaResponses = triviaResponses;
    }
    if(triviaQuestionNumber === triviaQuestions.length - 1) {
      finished = true;
    } else {
      triviaQuestionNumber++;
    }
  };

  const submitRiddleAnswer = () => {
    if(riddleAnswer === riddle.answer) {
      answeredCorrect = true;
    } else {
      answeredCorrect = false;
    }
  };

</script>

<main>
  <div class="lg:px-40 md:px-20 px-8 py-20">
    <div class="flex md:flex-row flex-col items-stretch mb-4">
      <div class="md:w-1/2 w-full p-2">
        <div class="bg-white shadow-md p-8 h-full">
          <p class="font-bold text-xl border-b pb-4 mb-4">{question}</p>
          {#each frameworks as framework}
            <div class="mb-4">
              <p class="mr-4 font-bold text-gray-600">{framework.name}</p>
              <div class="flex">
              <!-- <p class="font-bold">{totalVotes === 0 ? 0 : framework.votes/totalVotes * 100}</p> -->
                <div class="w-full bg-gray-100 h-6">
                  <div class={`h-full bg-${framework.color}`} style={`width: ${totalVotes === 0 ? 0 : framework.votes/totalVotes * 100}%`}></div>
                </div>
                <button class="ml-4 rounded px-2 bg-indigo-500 text-white" on:click={() => {addVote(framework.name)}}>Vote</button>
              </div>
            </div>
          {/each}
        </div>
      </div>
      <div class="md:w-1/2 w-full p-2">
        <div class="bg-white shadow-md p-8 h-full">
          <p class="font-bold text-xl border-b pb-4 mb-4">{triviaQuestions[triviaQuestionNumber].question}</p>
          <div>
            {#if !finished}
            {#each triviaQuestions[triviaQuestionNumber].options as option}
              <div on:click={() => {selectOption(triviaQuestions[triviaQuestionNumber].answer, option.id)}} class="w-full bg-gray-50 rounded-md mb-2 p-4">
                {option.option}
              </div>
            {/each}
            {:else}
            <div>
              <div class="text-center text-lg font-bold mb-8">Finished!</div>
              <div class="p-4 bg-indigo-100 rounded-md text-center text-5xl text-indigo-500 font-black">{triviaResponses.length}/{triviaQuestions.length}</div>
            </div>
            {/if}
          </div>
        </div>
      </div>
    </div>

    <div class="w-full p-2">
      <div class="bg-white shadow-md p-8">
        {#if answeredCorrect === undefined}
        <RiddleCard question={riddle.question} bind:answer={riddleAnswer} submit={submitRiddleAnswer}/>
        {:else}
        <div class="w-full flex flex-col items-center justify-center">
          <div class={`w-full text-center font-bold text-xl border-b pb-4 mb-4 ${answeredCorrect ? 'text-green-500' : 'text-red-500'}`}>{answeredCorrect ? 'Correct!' : 'Incorrect :('}</div>
          <div>Correct Answer: <span class="font-bold">{riddle.answer}</span></div>
          <div class="text-gray-500">Your Answer: <span class="font-bold">{riddleAnswer}</span></div>
        </div>
        {/if}
      </div>
    </div>
  </div>
</main>
