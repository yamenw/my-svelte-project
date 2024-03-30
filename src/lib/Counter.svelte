<script lang="ts">
  const images: string[] = [];
  for (let index = 0; index < 27; index++) {
    images.push(`images/frame${index}.webp`);
  }
  let count: number = 0;
  let frame: number = 0;
  let score: number = 0;
  let interval: number;
  const incrementFrame = () => {
    frame = (frame + 1) % images.length;
  };
  const updateInterval = () => {
    clearInterval(interval);
    interval = setInterval(incrementFrame, 1000 / (images.length * count));
  };
  const increment = () => {
    count += 1;
    score = Math.max(score, count);
    updateInterval();
    setTimeout(() => {
      count--;
      updateInterval();
      if (count === 0) {
        clearInterval(interval);
        frame = 0;
      }
    }, 1000);
  };
</script>

<p style="color: red;">Mash the boogie button to progress</p>
<h3>Max score: {score} boogies per second</h3>
<div class="container">
  current boogie speed is {count} boogies per second
  <br />
  <button on:click={increment}> boogie </button>
  <img src={images[frame]} width="640" height="578" alt="" />
</div>

<div style="--speed:{count}s;"></div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: auto;
    gap: 16px;
  }
</style>
