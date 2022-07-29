<script>
  import { each } from 'svelte/internal';

  import Card2 from './Card2.svelte';

  let hand = ['AS', '2S', '5H'];
  let medianIndex = Math.floor(hand.length / 2);
  let panAngle = 45 / hand.length;
  let panMedian = 90 / 2;
  let panAngleLeft = -30;
  let panAngleRight = 30;

  function computeCardPan(index) {
    if (index < medianIndex) {
      return (panAngleLeft += 10);
    } else if (index > medianIndex) {
      return (panAngleRight -= 10);
    } else {
      return 0;
    }
  }
</script>

<div class="hand">
  {#each hand as card, idx}
    <div style="--pan-angle:{computeCardPan(idx)}deg; --transform-origin: {idx < medianIndex ? 'top left' : 'top right'}">
      <Card2 cid="{card}" />
      {idx}
    </div>
  {/each}
</div>

<style>
  .hand {
    display: flex;
    flex-direction: row;
  }
</style>
