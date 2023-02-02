<script lang="ts">
  let newCardTitle = "";
  let newCardText = "";
  let cards = [];
  let status = false;
  let date = new Date();

  function addCard() {
    newCardTitle === "" || newCardText == ""
      ? alert("Please fill in all fields")
      : (cards = [
          ...cards,
          {
            title: newCardTitle,
            text: newCardText,
            status: status,
            date: date.toLocaleDateString(),
          },
        ]);
    localStorage.setItem("cards", JSON.stringify(cards));
    (newCardTitle = ""), (newCardText = "");
  }

  function removeCard(index) {
    cards.splice(index, 1);
    localStorage.setItem("cards", JSON.stringify(cards));
    cards = cards;
  }

  const storedCards = localStorage.getItem("cards");
  storedCards ? (cards = JSON.parse(storedCards)) : (cards = []);
</script>

<main class="main">
  <div class="pt-2">
    <input
      bind:value={newCardTitle}
      type="text"
      placeholder="New task name"
      class="input input-bordered input-success "
    />
  </div>

  <div class="pt-2">
    <input
      bind:value={newCardText}
      type="text"
      placeholder="New task description"
      class="input input-bordered input-success  "
    />
  </div>

  <div class="pt-2">
    <button on:click={addCard} class="btn btn-success btn-outline "
      >Add new task</button
    >
  </div>

  <div class="flex justify-center flex-wrap">
    {#each cards as card, index}
      <div class="card border border-black bg-amber-300">
        <div class="card-actions justify-between">
          <button
            class="btn btn-xs btn-square btn-error"
            on:click={() => removeCard(index)}>❌</button
          >
          <button
            on:click={() => {
              card.status = !card.status;
              localStorage.setItem("cards", JSON.stringify(cards));
            }}
            class="btn btn-xs btn-square btn-success">✅</button
          >
        </div>
        <div class="card-body text-center">
          <h1 class="card-title text-black">{card.title}</h1>
          <p class="text-black">{card.text}</p>
          <p class="text-black">{card.date}</p>
          <p class="text-black">{card.status ? "Completed" : "Uncomplete"}</p>
        </div>
      </div>
    {/each}
  </div>
</main>
