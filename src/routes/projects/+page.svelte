<script>
    import projects from "$lib/projects.json";
    import Project from "$lib/Project.svelte";
    import Pie from '$lib/Pie.svelte';
    import * as d3 from 'd3'; 

    let rolledData = d3.rollups(projects, v => v.length, d => d.year);

    let pieData = rolledData.map(([year, count]) => {
      return { value: count, label: year };
    });

</script>

<svelte:head>
  <title>Projects</title>
</svelte:head>

<Pie data={pieData}/>

<h1>{ projects.length } Projects</h1>
<div class="projects">
    {#each projects as p}
        <Project data={p}/>
      <!-- <article>
        <h2>{p.title}</h2>
        <img src={p.image} alt="" />
        <p>
            {p.description}
        </p>
      </article> -->
    {/each}
</div>