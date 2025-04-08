
<script>
    
    import { base } from "$app/paths";
    import { page } from "$app/stores";
    
    
    let pages = [
        { url: "/", title: "Home" },
        { url: "/projects", title: "Projects" },
        { url: "/contact", title: "Contact" },
        { url: "/resume", title: "Resume" },
        { url: "/meta", title: "Meta" },
        {url: "https://github.com/LuuSamp", title:"Github"}
    ];
    
    let localStorage = globalThis.localStorage ?? {};
    
    let colorScheme = localStorage.colorScheme ?? "light dark";
    let root = globalThis?.document?.documentElement;
    
    $: root?.style.setProperty("color-scheme", colorScheme);
    $: localStorage.colorScheme = colorScheme;
    
</script>

<nav>
    {#each pages as p}
    <a
    href={p.url.startsWith("http") ? p.url: `${base}${p.url}`}
    class:current={$page.route.id === p.url}
    target={p.url.startsWith("http") ? "_blank" : undefined}
    >
    {p.title}
    </a>

    {/each}
  </nav>
  

  <label class="color-scheme">
    Theme:
    <select bind:value={colorScheme}>
        <option value="light dark"> Automatic </option>
        <option value="light"> Light </option>
        <option value="dark"> Dark </option>
    </select>
</label>



<slot />

<style>

nav {
	display: flex; /* Display the navigation bar as a flex container */
	border-bottom-width: 1px;
	border-bottom-style: solid;
	border-bottom-color: oklch(80% 3% 200);
}

nav a {
	flex:1;
	text-decoration: none;
	color: inherit;
	text-align: center;
	padding: 0.5em;
}

nav .current{
	border-bottom-width: 0.4em;
	border-bottom-style: solid;
	border-bottom-color: var(--grey);
	padding: 0.1em;
}

nav a:hover {
	border-bottom-width: 0.1em;
	border-bottom-style: solid;
	border-bottom-color: var(--color-accent);
	padding-bottom: -0.1em;
	background-color: var(--color-accent-bg);
}

.color-scheme{
    position:absolute;
    top: 1rem;
    right: 1rem;
    display: inline-flex;
    gap: 5px;
}

</style>