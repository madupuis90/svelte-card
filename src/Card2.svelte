<script>
  export let cid;

  let flipped = false;
</script>

<div class="card" class:flipped on:click="{() => (flipped = !flipped)}">
  <img class="card__face card__face--front" src="/cards/{cid.toUpperCase()}.svg" alt="{cid}" />
  <div class="card__face card__face--back"></div>
</div>

<style>
  :root {
    /* variables  */
    --card-size: 10em;
    --card-size-ratio: calc(3.5 / 2.5);
    /* perspective: 600px; */
  }
  .card {
    width: var(--card-size);
    height: calc(var(--card-size) * var(--card-size-ratio));
    transition: transform 0.5s;
    transition-timing-function: ease-out;
    transform-style: preserve-3d;
    /* transform-origin: (var(--transform-origin, 0 0));   */
    transform: rotateZ(var(--pan-angle));
  }

  .card__face {
    width: 100%;
    height: 100%;
    border: 1px solid black;
    border-radius: 10px;
    position: absolute;
    backface-visibility: hidden;
  }

  .card__face--front {
    width: 100%;
  }

  .card__face--back {
    transform: rotateY(180deg);
    background: repeating-linear-gradient(45deg, #606dbc, #606dbc 10px, #465298 10px, #465298 20px);
  }

  .card.flipped {
    transform: translateX(100%) rotateY(180deg);
    /* transform: rotateY(180deg) translateX(100%); */
  }
</style>
