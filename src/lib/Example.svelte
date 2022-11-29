<script>
  import data from '../data/data.json';
  import Line from '../lib/Line.svelte';
  console.log(data);
  import {scaleLinear, scaleTime} from 'd3-scale';
  import AxisX from './axisX.svelte';
  import AxisY from './axisY.svelte';

  let height = 400;

  let width = 450;

  let minDate = new Date('2020/06/01');
  let maxDate = new Date('2020/11/03');
  const margin = {
    top: 30,
    right: 50,
    bottom: 30,
    left: 50,
  };
  let innerHeight = height - margin.top - margin.bottom;
  let innerWidth = width - margin.left - margin.right;
  const xScale = scaleTime()
    .domain([minDate, maxDate]) // INPUT
    .range([0, innerWidth]); // OUTPUT
  const yScale = scaleLinear()
    .domain([0, 100]) // INPUT
    .range([innerHeight, 0]); // OUTPUT
</script>

<svg {width} {height}>
  <g transform={`translate(${margin.left}, ${margin.top})`}>
    <Line {xScale} {yScale} data={data.Biden} color="blue" />
    <Line {xScale} {yScale} data={data.Trump} color="red" />
    <AxisX {xScale} height={innerHeight} />
    <AxisY {yScale} width={innerWidth} />
  </g></svg
>
