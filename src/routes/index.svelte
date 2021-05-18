<script lang="ts">
  import { onMount } from 'svelte';

  type Dot = {
    x: number;
    y: number;
    size: number;
    color: string;
  };

  let dots: Dot[] = [];
  let container: Element = null;

  function random(limit) {
    return Math.floor(Math.random() * limit);
  }

  function pickColor() {
    const colors = ['#f7f3e9', '#a3d2ca', '#5eaaa8', '#f05945'];
    const index = Math.floor(random(colors.length));

    return colors[index];
  }

  function seed() {
    const width = container.clientWidth;
    const height = container.clientHeight;

    dots = [...Array(300)].map((i) => {
      return {
        x: random(width) - 20,
        y: random(height) - 20,
        size: random(30) + 10,
        color: pickColor()
      };
    });
  }

  onMount(() => {
    seed();
  });
</script>

<div class="container" bind:this={container}>
  {#each dots as dot}
    <div class="dot" style="--x: {dot.x}px; --y: {dot.y}px; --size: {dot.size}px; --color: {dot.color}" />
  {/each}
</div>

<style>
  .container {
    width: 100vw;
    height: 100vh;
    position: relative;
    overflow: hidden;
  }

  .dot {
    position: absolute;
    transform: translate(var(--x), var(--y));
    background-color: var(--color);
    width: var(--size);
    height: var(--size);
    border-radius: 50%;
  }
</style>
