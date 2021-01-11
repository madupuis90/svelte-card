<script>
  let flipped = false;
</script>

<div class="scene">
  <div class="card" class:flipped on:click={() => flipped = !flipped}>
    <div class="card__face card__face--front"></div>
    <div class="card__face card__face--back"></div>
  </div>
</div>

<style>
  .scene {
    width: 200px;
    height: 260px;
    perspective: 600px;
  }

  .card {
    width: 100%;
    height: 100%;
    position:relative;
    transition: transform 1s;
    transform-style: preserve-3d;
  }

  .card__face {
    width: 100%;
    height: 100%;
    position: absolute;
    backface-visibility: hidden;
  }

  .card__face--front {
    background-color: red;
  }

  .card__face--back {
    background-color: blue;
    transform: rotateY(180deg);
  }

  .card.flipped {
    transform: rotateY(180deg);
  }
</style>