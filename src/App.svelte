<script>
	import { navOptions } from "./Navbar.svelte";

	let selected = navOptions[0];
	// let intSelected = 0; // selected page index

	function changeComponent(event) {
		selected = navOptions[event.srcElement.id];
		// intSelected = event.srcElement.id;
	}
</script>

<main>
	<header>
		<div><img src="/assets/shared/logo.svg" alt="star is born" /></div>
		<nav>
			<ul>
				{#each navOptions as option, i}
					<li>
						<a href={option.url} on:click={changeComponent} id={i}
							><span class="number-navbar-link">0{i}</span
							>{option.page}</a
						>
					</li>
				{/each}
			</ul>
		</nav>
	</header>

	<svelte:component this={selected.component} />
</main>

<style>
	main {
		min-height: 100vh;
		width: 100vw;
		background-color: black;
	}

	header {
		position: fixed;
		right: 0;
		top: 10%;
		height: max-content;
		width: 100%;
		display: flex;
		align-items: center;
	}

	header div {
		width: 180px;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	nav {
		backdrop-filter: blur(20px);
		-webkit-backdrop-filter: blur(20px);
		box-shadow: inset 0 0 2000px rgba(255, 255, 255, 0.1);
		display: flex;
		justify-content: center;
		align-items: center;
		width: 800px;
		margin-left: auto;
	}

	nav::before {
		content: "";
		display: block;
		position: absolute;
		height: 1.5px;
		width: calc(100vw - 120%);
		right: -20px;
		margin-right: 100%;
		background-color: rgba(255, 255, 255, 0.1);
	}

	nav ul {
		position: relative;
		display: flex;
		justify-content: space-around;
		align-items: center;
		list-style: none;
		height: 80px;
		width: 600px;
	}

	nav ul li,
	nav ul li a {
		height: 100%;
		width: auto;
	}

	nav ul li a {
		font-family: "Barlow";
		font-size: 12px;
		color: white;
		text-decoration: none;
		letter-spacing: 2px;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	nav ul li:hover {
		height: calc(100% - 2px);
		border-bottom: 2px solid white;
		margin-bottom: -2px;
	}

	nav ul li a span.number-navbar-link {
		font-weight: 900;
		margin-right: 8px;
	}

	@media (max-width: 50rem) {
		header {
			top: 0;
		}
		nav::before {
			display: none;
		}
	}
</style>
