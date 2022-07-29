<script>
  export let suit;
  export let value;

  let flipped = false;

  const suits = {
    spade: { unicode: '♠', color: 'black' },
    club: { unicode: '♣', color: 'black' },
    heart: { unicode: '♥', color: 'red' },
    diamond: { unicode: '♦', color: 'red' },
    joker: { unicode: '', color: 'black' },
  };

  const patterns = {
    1: [{ x: 0, y: 0 }],
    2: [
      { x: 0, y: -1 },
      { x: 0, y: 1, mirrored: true },
    ],
    3: [
      { x: 0, y: -1 },
      { x: 0, y: 0 },
      { x: 0, y: 1, mirrored: true },
    ],
    4: [
      { x: -1, y: -1 },
      { x: -1, y: 1, mirrored: true },
      { x: 1, y: -1 },
      { x: 1, y: 1, mirrored: true },
    ],
    5: [
      { x: -1, y: -1 },
      { x: -1, y: 1, mirrored: true },
      { x: 0, y: 0 },
      { x: 1, y: -1 },
      { x: 1, y: 1, mirrored: true },
    ],
    6: [
      { x: -1, y: 1, mirrored: true },
      { x: -1, y: -1 },
      { x: -1, y: 0 },
      { x: 1, y: 0 },
      { x: 1, y: -1 },
      { x: 1, y: 1, mirrored: true },
    ],
    7: [
      { x: -1, y: 1, mirrored: true },
      { x: -1, y: -1 },
      { x: -1, y: 0 },
      { x: 0, y: -1 / 2 },
      { x: 1, y: 0 },
      { x: 1, y: -1 },
      { x: 1, y: 1, mirrored: true },
    ],
    8: [
      { x: -1, y: 1, mirrored: true },
      { x: -1, y: -1 },
      { x: -1, y: 0 },
      { x: 0, y: -1 / 2 },
      { x: 0, y: 1 / 2, mirrored: true },
      { x: 1, y: 0 },
      { x: 1, y: -1 },
      { x: 1, y: 1, mirrored: true },
    ],
    9: [
      { x: -1, y: -1 },
      { x: -1, y: -1 / 3 },
      { x: -1, y: 1, mirrored: true },
      { x: -1, y: 1 / 3, mirrored: true },
      { x: 0, y: 0 },
      { x: 1, y: -1 },
      { x: 1, y: -1 / 3 },
      { x: 1, y: 1, mirrored: true },
      { x: 1, y: 1 / 3, mirrored: true },
    ],
    10: [
      { x: -1, y: -1 },
      { x: -1, y: 1, mirrored: true },
      { x: -1, y: 1 / 3, mirrored: true },
      { x: -1, y: -1 / 3 },
      { x: 0, y: -2 / 3 },
      { x: 0, y: 2 / 3, mirrored: true },
      { x: 1, y: -1 / 3 },
      { x: 1, y: 1 / 3, mirrored: true },
      { x: 1, y: 1, mirrored: true },
      { x: 1, y: -1 },
    ],
  };
  const s = suits[suit];
  const pattern = typeof value === 'number' && value > 0 && value < 11 ? patterns[value] : patterns[1];
</script>

<div class="scene">
  <div class="card {s.color}" class:flipped on:click="{() => (flipped = !flipped)}">
    <div class="card__face card__face--front">
      <div class="card__header card__header--top">
        <span>{value}</span>
        <span>{s.unicode}</span>
      </div>

      <div class="card__pattern">
        {#if value === 'J'}
          <div class="symbol figure">♙</div>
        {:else if value === 'Q'}
          <div class="symbol figure">♕</div>
        {:else if value === 'K'}
          <div class="symbol figure">♔</div>
        {:else if value === 'JOKER'}
          <div class="symbol figure">🃏</div>
        {:else}
          {#each pattern as symbol}
            <div class="symbol {symbol.mirrored ? 'mirrored' : ''}" style="left: {symbol.x * 100}%; top: {symbol.y * 100}%">
              {s.unicode}
            </div>
          {/each}
        {/if}
      </div>

      <div class="card__header card__header--bottom mirrored">
        <span>{value}</span>
        <span>{s.unicode}</span>
      </div>
    </div>
    <div class="card__face card__face--back"></div>
  </div>
</div>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Oranienbaum&display=swap');

  .scene {
    font-size: 48px;
    width: 4em;
    height: 6em;
    perspective: 600px;
  }

  .card {
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    transform-origin: center left;
  }

  .card.flipped {
    transform: translateX(100%) rotateY(-180deg);
  }

  .card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    border: 2px solid black;
    border-radius: 25px;
    box-shadow: 4px -2px 8px 2px lightgray;
    cursor: default;
    -moz-user-select: none;
    -webkit-user-select: none;
    backface-visibility: hidden;
  }

  .card__face--front {
    font-family: 'Oranienbaum', serif;
    background-color: white;
  }

  .card__face--back {
    background: repeating-linear-gradient(45deg, #606dbc, #606dbc 10px, #465298 10px, #465298 20px);
    transform: rotateY(180deg);
  }

  .card__header {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 4px 2px;
    line-height: 1em;
  }

  .card__header--top {
    top: 0;
    left: 0;
  }

  .card__header--bottom {
    bottom: 0;
    right: 0;
  }

  .card__pattern {
    font-size: 64px;
    position: absolute;
    left: 50%;
    top: 50%;
    width: 20%;
    height: 30%;
    transform: translate(-50%, -50%);
  }

  .red {
    color: red;
  }

  .black {
    color: black;
  }

  .mirrored {
    transform: rotate(180deg);
  }

  .symbol {
    position: absolute;
  }

  .figure {
    left: -115%;
    top: -52%;
    font-size: 2em;
  }
</style>
