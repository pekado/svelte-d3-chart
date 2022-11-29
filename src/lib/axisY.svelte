<script>
  export let yScale;
  export let width;
</script>

{#each yScale.ticks(5) as tick}
  <text
    y={yScale(tick)}
    x={0}
    fill="black"
    text-anchor="end"
    dominant-baseline="middle"
    dx="-6">{tick}{tick === 100 ? '%' : ''}</text
  >
  <line
    x1="0"
    x2={width}
    y1={yScale(tick)}
    y2={yScale(tick)}
    stroke="black"
    stroke-width="0.5"
  />
{/each}
