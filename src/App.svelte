<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import PollList from "./components/PollList.svelte";

  // tabs
  let items = [
    { id: 1, name: "Current Polls" },
    { id: 2, name: "Add New Poll" },
  ];
  let activeItem = "Current Polls";

  const tabChange = (e) => {
    activeItem = e.detail.name;
  };

  let polls = [];

  const submitPollForm = (e) => {
    const poll = {};
    poll.id = e.detail.id;
    poll.question = e.detail.question;
    poll.answerA = e.detail.answerA;
    poll.answerB = e.detail.answerB;
    poll.voteA = e.detail.voteA;
    poll.voteB = e.detail.voteB;
    polls = [poll, ...polls];
    console.log(polls);
    activeItem = "Current Polls";
  };

  const handleVote = (e) => {
    const { id, option } = e.detail;
    
    let copiedPoll = [...polls];
    let updatePoll = copiedPoll.find(poll => poll.id == id);
    if (option === "a") {
      updatePoll.voteA++;
    } else {
      updatePoll.voteB++;
    }
    polls = copiedPoll
  };
</script>

<Header />
<main>
  <!-- Tabs component dispatch event 'tabChange' to this file -->
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === "Current Polls"}
    <PollList {polls} on:vote={handleVote} />
  {:else if activeItem === "Add New Poll"}
    <CreatePollForm on:submitPollForm={submitPollForm} />
  {/if}
</main>
<Footer />

<style>
  main {
    width: 100%;
    max-width: 960px;
    margin: 40px auto;
  }
</style>
