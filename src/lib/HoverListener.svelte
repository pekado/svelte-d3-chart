<script>
  export let xScale;
  export let margin;
  export let width;
  export let height;
  export let hoveredDate;
  const handleMousemove = function (e) {
    console.log(e);
    hoveredDate = xScale.invert(e.offsetX - margin.left);
  };
</script>

<rect
  class="hover-listener"
  fill="transparent"
  {width}
  {height}
  on:mousemove={handleMousemove}
/>

<line
  x1={xScale(hoveredDate)}
  x2={xScale(hoveredDate)}
  y1={0}
  y2={height}
  stroke="darkgrey"
  stroke-dasharray="2, 2"
  pointer-events="none"
/>

<style>
  rect {
    cursor: crosshair;
  }
</style>
