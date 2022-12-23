# Svelte Card

This project was to play around with Svelte and CSS. The goal was to create a card component that can be flipped (3d). 

## Code
The `card.svelte` component was the first iteration where I create the card using only html/css. This works until you need to make the figures. 

The `card.svelte` is the second version and uses open source SVGs to for the card, this version is a lot simpler and handles figures.

The cards can be flipped by clicking on them. The way it works is that the card is actually 2x div overlapping and facing opposite direction. By enabling 3d in CSS, this allows you to see both sides of the card during the flip animation
