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
    activeItem = "Current Polls";
  };
</script>

<Header />
<main>
  <!-- Tabs component dispatch event 'tabChange' to this file -->
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === "Current Polls"}
    <PollList />
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
