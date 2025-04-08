<svelte:head>
  <title>Home</title>
</svelte:head>

<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
  import { onMount } from "svelte";

  let githubData = null;
  let loading = true;
  let error = null;

  onMount(async () => {
      try {
          const response = await fetch("https://api.github.com/users/LuuSamp");
          githubData = await response.json();
      } catch (err) {
          error = err;
      }
      loading = false;
  });


</script>

<!-- <h1> (Heading 1) represents the main heading of a webpage or a section.-->
<h1> LUCIANO PEREIRA SAMPAIO </h1>

<!-- <nav> (Navigation) is used to create a menu with links to other pages or external sites. -->
    <!-- <nav>
        <a href="index.html">Home</a>
        <a href="./projects/">Projects</a>
        <a href="./contact/">Contact</a>

    </nav> -->

<!-- <p> (Paragraph) represents a paragraph of text.-->
<p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque felis ante, finibus eget libero et, commodo lacinia nulla. Mauris mi felis, maximus a pulvinar at, mollis ac enim. Integer accumsan leo non tristique ullamcorper. Aenean facilisis dui libero, sagittis luctus diam placerat non. Mauris libero massa, ullamcorper eget ultrices vitae, hendrerit a ipsum. Quisque mi neque, convallis condimentum sagittis nec, luctus id ligula. Aliquam tincidunt molestie odio vel venenatis. Morbi quis turpis diam. Donec non rhoncus tellus, at varius lacus. </p>

<!-- <img> (Image) tag is used to display images.-->
<img src="images/my_image.jpeg" alt="DICE!!" width="700" height="600">


{#if loading}
    <p>Loading...</p>
{:else if error}
    <p class="error">Something went wrong: {error.message}</p>
{:else}
    <section>
        <h2>My GitHub Stats</h2>
        <dl>
            <dt>Followers</dt>
            <dd>{githubData.followers}</dd>
            <dt>Following</dt>
            <dd>{githubData.following}</dd>
            <dt>Public Repositories</dt>
            <dd>{githubData.public_repos}</dd>
        </dl>
    </section>
{/if}

<h2>
  Latest Projects
</h2>
<div class="projects">
{#each projects.slice(0, 3) as p}
  <Project data={p} hLevel="3"/>
{/each}
</div>