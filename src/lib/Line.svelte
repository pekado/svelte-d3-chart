<script>
  export let xScale;
  export let yScale;
  export let data;
  export let color;

  import {line} from 'd3-shape';
  $: lineGenerator = line()
    .x((d) => xScale(new Date(d.date)))
    .y((d) => yScale(d.winprob));
</script>

<path
  d={lineGenerator(data)}
  fill="transparent"
  stroke={color}
  stroke-width="4"
/>
