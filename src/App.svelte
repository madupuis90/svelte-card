<script>
  import Card from './Card.svelte';
import Card2 from './Card2.svelte';
</script>

<Card value="A" suit=club></Card>
<Card value={2} suit=heart></Card>
<Card value={3} suit=spade></Card>
<!-- <Card value={4} suit=spade></Card>
<Card value={5} suit=spade></Card>
<Card value={6} suit=spade></Card>
<Card value={7} suit=spade></Card>
<Card value={8} suit=spade></Card>
<Card value={9} suit=spade></Card>
<Card value={10} suit=spade></Card>
<Card value="J" suit=spade></Card>
<Card value="Q" suit=spade></Card>
<Card value="K" suit=spade></Card> -->


<!-- <Card2></Card2>
<Card2></Card2>
<Card2></Card2> -->
<style>
  :global(body) {
    background-color:rgb(124, 189, 124);
  }
</style>