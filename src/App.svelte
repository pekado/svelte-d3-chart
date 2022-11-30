<script>
  import data from './data/data.json';
  import Line from './lib/Line.svelte';
  import {scaleLinear, scaleTime} from 'd3-scale';
  import AxisX from './lib/axisX.svelte';
  import AxisY from './lib/axisY.svelte';
  import HoverListener from './lib/HoverListener.svelte';
  import Tooltip from './lib/Tooltip.svelte';
  const margin = {
    top: 30,
    right: 50,
    bottom: 30,
    left: 50,
  };
  let height = 400;
  let width = 450;
  const BIDEN_COLOR = '#5768ac';
  const TRUMP_COLOR = '#fa5a50';

  const minDate = new Date(data.Biden[0].date);
  const maxDate = new Date(data.Biden[data.Biden.length - 1].date);

  let hoveredDate = maxDate;
  let innerHeight = height - margin.top - margin.bottom;
  $: innerWidth = width - margin.left - margin.right;
  $: xScale = scaleTime()
    .domain([minDate, maxDate]) // INPUT
    .range([0, innerWidth]); // OUTPUT

  const yScale = scaleLinear()
    .domain([0, 100]) // INPUT
    .range([innerHeight, 0]); // OUTPUT
</script>

<div bind:clientWidth={width}>
  <svg {width} {height}>
    <g transform={`translate(${margin.left}, ${margin.top})`}>
      <Line {xScale} {yScale} data={data.Biden} color="blue" />
      <Line {xScale} {yScale} data={data.Trump} color="red" />
      <AxisX {xScale} height={innerHeight} />
      <AxisY {yScale} width={innerWidth} />
      <HoverListener
        width={innerWidth}
        height={innerHeight}
        {xScale}
        {margin}
        bind:hoveredDate
      />
      <Tooltip
        {hoveredDate}
        {xScale}
        {yScale}
        data={data.Biden}
        color={BIDEN_COLOR}
      />
      <Tooltip
        {hoveredDate}
        {xScale}
        {yScale}
        data={data.Trump}
        color={TRUMP_COLOR}
      />
    </g></svg
  >
</div>
