<script>
	import { onMount } from "svelte";

	import { navOptions } from "./Navbar.svelte";

	$: selected = navOptions[0];

	const allLinks = document.getElementsByClassName("link");

	onMount(() => {
		window.addEventListener("resize", () => {
			document
				.querySelector(":root")
				.style.setProperty("--vh", window.innerHeight / 100 + "px");
		});

		document
			.querySelector(":root")
			.style.setProperty("--vh", window.innerHeight / 100 + "px");

		if (allLinks.length > 0) {
			allLinks[0].classList.add("active");
		}
		for (let i = 0; i < navOptions.length; i++) {
			if (navOptions[i].url === window.location.pathname) {
				selected = navOptions[i];
			}
		}
	});

	let isOpen = false;

	$: innerWidth = 0;

	function changeComponent(event) {
		event.preventDefault();
		selected = navOptions[event.srcElement.id];
		for (let y = 0; y < allLinks.length; y++) {
			for (let i = 0; i < allLinks[y].classList.length; i++) {
				if (allLinks[y].classList[i] === "active") {
					allLinks[y].classList.remove("active");
				}
			}
		}
		event.target.parentNode.classList.add("active");
		isOpen = !isOpen;
	}

	function toggleNavigation() {
		isOpen = !isOpen;
	}
</script>

<svelte:window bind:innerWidth />

<main>
	<header>
		<div id="logo-header-container">
			<img src="/assets/shared/logo.svg" alt="star is born" />
		</div>
		<nav
			class="nav {(innerWidth < 520 && isOpen) || innerWidth > 520
				? `show`
				: `hidden`}"
		>
			<ul>
				{#each navOptions as option, i}
					<li class={navOptions[i] === i ? "link active" : "link"}>
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
					src={isOpen
						? "/assets/shared/icon-close.svg"
						: "/assets/shared/icon-hamburger.svg"}
				/></button
			>
		</div>
	</header>

	<svelte:component this={selected.component} />
</main>

<style>
	main {
		min-height: calc(100 * var(--vh));
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
		-webkit-box-shadow: inset 0 0 2000px rgba(255, 255, 255, 0.1);
		box-shadow: inset 0 0 2000px rgba(255, 255, 255, 0.1);
		display: -webkit-box;
		display: -ms-flexbox;
		display: flex;
		-webkit-box-pack: center;
		-ms-flex-pack: center;
		justify-content: center;
		-webkit-box-align: center;
		-ms-flex-align: center;
		align-items: center;
		width: 800px;
		margin-left: auto;
		position: relative;
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
	.show {
		display: flex;
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
		border-bottom: 2px solid lightslategray;
		margin-bottom: -2px;
	}

	.link.active {
		height: calc(100% - 2px);
		border-bottom: 2px solid white;
		margin-bottom: -2px;
	}

	nav ul li a span.number-navbar-link {
		font-family: "Barlow-Bold";
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
			z-index: 10;
			height: 100px;
		}

		nav ul {
			height: calc(100 * var(--vh));
			flex-direction: column;
			padding: 0;
		}

		.nav.hidden {
			transition: all 1s;
			transform: translateX(150%);
			position: absolute;
			display: flex;
			height: calc(100 * var(--vh));
			z-index: 1000;
			top: 0;
			padding: 20px;
			width: 75%;
			right: 0;
			align-items: flex-start;
		}
		.nav.hidden ul {
			height: auto;
			margin-top: 50px;
		}
		.nav.hidden ul li {
			width: 100%;
		}
		.nav.hidden ul li a {
			display: flex;
			align-items: center;
			justify-content: flex-start;
			padding: 20px;
			text-shadow: 1px 1px 2px black, 0 0 1em black, 0 0 0.2em black;
		}
		.nav.show {
			transition: all 1s;
			transform: translateX(0);
			position: absolute;
			display: flex;
			height: calc(100 * var(--vh));
			z-index: 1000;
			top: 0;
			padding: 20px;
			width: 75%;
			right: 0;
			align-items: flex-start;
		}
		.nav.show ul {
			height: auto;
			margin-top: 50px;
		}
		.nav.show ul li {
			width: 100%;
		}
		.nav.show ul li a {
			display: flex;
			align-items: center;
			justify-content: flex-start;
			padding: 20px;

			text-shadow: 1px 1px 2px black, 0 0 1em black, 0 0 0.2em black;
		}

		nav ul li a span.number-navbar-link {
			display: flex;
		}

		#logo-header-container {
			justify-content: flex-start;
		}
		#toggle-button-nav {
			display: flex;
			justify-content: flex-end;
			align-items: center;
			z-index: 1000;
		}
	}
	@media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
		header {
			padding: 20px;
			z-index: 10;
			height: 100px;
		}
		#logo-header-container {
			justify-content: flex-start;
			align-self: baseline;
		}
		/* nav {
			display: none;
		} */
		.nav.show {
			transition: all 1s;
			transform: translateX(0);
			position: absolute;
			display: flex;
			height: calc(100 * var(--vh));
			z-index: 1000;
			top: 0;
			width: 75%;
			right: 0;
		}
		.nav.show ul li {
			width: 100%;
		}
		.nav.show ul li a {
			display: flex;
			align-items: center;
			justify-content: flex-start;
			text-shadow: 1px 1px 2px black, 0 0 1em black, 0 0 0.2em black;
		}
		.nav.hidden {
			transition: all 1s;
			transform: translateX(150%);
		}

		nav ul {
			height: calc(100 * var(--vh));
			flex-direction: column;
			padding: 0;
		}

		#toggle-button-nav {
			justify-content: flex-end;
			z-index: 1000;
		}
		#toggle-button-nav button {
			padding: auto;
			margin: 0;
		}
	}
</style>
