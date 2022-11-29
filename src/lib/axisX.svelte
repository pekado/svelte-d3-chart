<script>
  export let xScale;
  export let height;
  import {timeFormat} from 'd3-time-format';
  const dateFormat = timeFormat('%b %d');
</script>

{#each xScale.ticks() as tick}
  <text
    x={xScale(tick)}
    y={height}
    fill="black"
    dy="12"
    dominant-baseline="hanging"
    text-anchor="middle">{dateFormat(tick)}</text
  >
{/each}
