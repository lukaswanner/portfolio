<script lang="ts">
  export let skills: string[];

  let cardsWrapper: HTMLElement;

  let cards: HTMLElement[] = [];
</script>

<ul
  bind:this={cardsWrapper}
  class="cards"
  on:mousemove={(e) => {
    cards.forEach((card) => {
      const rect = card.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;

      card.style.setProperty("--xPos", `${x}px`);
      card.style.setProperty("--yPos", `${y}px`);
    });
  }}
>
  {#each skills as skill, index}
    <li bind:this={cards[index]} class="mention-card">
      <div class="card-content">
        <p>{skill}</p>
      </div>
    </li>
  {/each}
</ul>

<style>
  /* ====================================================== */

  .cards {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 0.5rem;
  }

  .mention-card {
    height: 15rem;
    width: 20rem;
    display: flex;
    justify-content: center;
    align-items: center;

    border-radius: 1.5rem;
    color: var(--gray-300);
    background: radial-gradient(
      100rem circle at var(--xPos) var(--yPos),
      rgba(var(--accent-regular-rgb), 0),
      transparent 0%
    );

    position: relative;
    transition: all 0.15s;
  }

  .mention-card:hover {
    background: radial-gradient(
      100rem circle at var(--xPos) var(--yPos),
      rgba(var(--accent-regular-rgb), 0.8),
      transparent 15%
    );

    scale: 0.98;
  }
  .mention-card:hover::before {
    opacity: 1;
  }
  .mention-card::before {
    content: "";

    position: absolute;
    inset: 0;
    border-radius: inherit;

    background: radial-gradient(
      50rem circle at var(--xPos) var(--yPos),
      rgba(var(--accent-regular-rgb), 0.1),
      transparent 35%
    );
    opacity: 0;
    transition: 0.25 all ease-in-out;
  }

  .card-content {
    display: flex;
    align-items: center;
    justify-content: center;

    background-color: var(--gray-900);
    border-radius: inherit;
    transition: all 0.25s;
    height: calc(100% - 0.15rem);
    width: calc(100% - 0.15rem);
  }
</style>
