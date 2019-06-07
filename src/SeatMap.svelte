<script>
  import * as d3 from "d3";
  import * as topojson from "topojson";
  import { onMount } from "svelte";
  import nswMap from "../public/NSW-2016-electorates.json";

  onMount(() => {
    console.log('here');
    const svg = d3.select("svg");
    const path = d3.geoPath();
    // d3.json("/NSW-2016-electorates.json", function(error, nswMap) {
    //   console.log('again');
    //   if (error) throw error;
      console.log(nswMap);
      svg.append("g")
          .attr("class", "electorates")
        .selectAll("path")
        .data(topojson.feature(nswMap, nswMap.objects.electorates).features)
        .enter().append("path")
          .attr("d", path);

      svg.append("path")
          .attr("class", "electorate-borders")
          .attr("d", d3.path(topojson.mesh(nswMap, nswMap.objects.electorates, function(a, b) { return a !== b; })));
    // });
  });

</script>

<h1>Seat map</h1>
<svg width="960" height="600" class="map-svg"></svg>

<style>
/* .map-svg {
  width: 100%;
  height: 500px;
} */
</style>
