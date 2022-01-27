<script>
	import { navOptions } from "./Navbar.svelte";

	let selected = navOptions[0];
	// let intSelected = 0; // selected page index

	let isOpen = false;

	console.log(isOpen);

	function changeComponent(event) {
		selected = navOptions[event.srcElement.id];
		// intSelected = event.srcElement.id;
	}

	function toggleNavigation() {
		isOpen = !isOpen;
	}
</script>

<main>
	<header>
		<div id="logo-header-container">
			<img src="/assets/shared/logo.svg" alt="star is born" />
		</div>
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
		<div id="toggle-button-nav">
			<button on:click={toggleNavigation}
				><img
					alt="open navigation button"
					src="/assets/shared/icon-hamburger.svg"
				/></button
			>
		</div>
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
	#toggle-button-nav {
		display: none;
		justify-content: flex-end;
	}
	#toggle-button-nav button {
		background-color: transparent;
		border: none;
	}

	@media (max-width: 50rem) {
		header {
			top: 0;
		}
		nav {
			width: 60%;
		}
		nav::before {
			display: none;
		}
		nav ul li a span.number-navbar-link {
			display: none;
		}
	}
	@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
		header {
			top: 0;
		}
		nav {
			width: 500px;
		}
		nav::before {
			display: none;
		}
		nav ul li a span.number-navbar-link {
			display: none;
		}
	}
	@media only screen and (max-width: 520px) {
		header {
			padding: 20px;
			justify-content: space-around;
		}
		nav {
			display: none;
		}
		#logo-header-container {
			justify-content: flex-start;
		}
		#toggle-button-nav {
			display: flex;
			justify-content: flex-end;
			align-items: center;
		}
	}
	@media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
		header {
			padding: 20px;
		}
		#logo-header-container {
			justify-content: flex-start;
		}
		nav {
			display: none;
		}

		#toggle-button-nav {
			display: flex;
			justify-content: flex-end;
			align-items: center;
		}
	}
</style>
