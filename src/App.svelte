<script>
  import Card from './Card.svelte';

  import Card2 from './Card2.svelte';
  import Hand from './Hand.svelte';

  function generateDeck() {
    let suits = ['C', 'D', 'S', 'H'];
    let ranks = ['A', '2', '3', '4', '5', '6', '7', '8', '9', 'T', 'J', 'Q', 'K'];
    let cards = [];

    ranks.forEach((rank) => {
      suits.forEach((suit) => {
        cards.push(rank + suit);
      });
    });

    return cards;
  }

  let cards = generateDeck();
</script>

<div class="flex">
  <!-- {#each cards as card}
    <Card2 cid="{card}" />
  {/each} -->
  <Hand />
</div>

<style>
  :global(body) {
    background-color: rgb(124, 189, 124);
  }
  .flex {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
</style>
