<script>
    import { onMount } from "svelte";
    import { technology } from "./data.json";

    const allLinks = document.getElementsByClassName("nested-link");

    $: innerHeight = 0;
    $: innerWidth = 0;
    $: deviceUsed = 0;

    onMount(() => {
        if (innerWidth <= 800 || innerWidth < innerHeight) {
            console.log("vue d'un téléphone");
            console.log(`height = ${innerHeight} and width = ${innerWidth}`);
            deviceUsed = 0;
        } else {
            console.log("vue d'un écran large");
            console.log(`height = ${innerHeight} and width = ${innerWidth}`);
            deviceUsed = 1;
        }
        if (allLinks.length > 0) {
            allLinks[0].classList.add("active");
        }
        for (let i = 0; i < technology.length; i++) {
            allLinks[i].firstElementChild.textContent = i + 1;
            if (technology[i].url === window.location.hash) {
                selected = technology[i];
            }
        }
    });

    $: nestedSelected = technology[0];

    function handleResizeWindow() {
        if (innerWidth <= 800 || innerWidth < innerHeight) {
            console.log("vue d'un téléphone");
            console.log(`height = ${innerHeight} and width = ${innerWidth}`);
            deviceUsed = 0;
        } else {
            console.log("vue d'un écran large");
            console.log(`height = ${innerHeight} and width = ${innerWidth}`);
            deviceUsed = 1;
        }
    }

    function handleNestedNavigation(event) {
        event.preventDefault();
        nestedSelected = technology[event.srcElement.id];

        for (let y = 0; y < allLinks.length; y++) {
            for (let i = 0; i < allLinks[y].classList.length; i++) {
                if (allLinks[y].classList[i] === "active") {
                    allLinks[y].classList.remove("active");
                }
            }
        }
        if (event.target.tagName === "A") {
            event.target.parentNode.classList.add("active");
        } else {
            event.target.classList.add("active");
        }
    }
</script>

<svelte:window
    bind:innerHeight
    bind:innerWidth
    on:resize={handleResizeWindow}
/>
<div id="technology">
    <div id="wrapper-grid-technology">
        <div id="header-technology">
            <h1><span>03</span>SPACE LUNCH 101</h1>
        </div>

        <div id="grid-technology">
            <div class="wrapper-image-grid">
                <img
                    src={deviceUsed === 1
                        ? nestedSelected.images.portrait
                        : nestedSelected.images.landscape}
                    alt="image de {nestedSelected.name}"
                />
            </div>
            <div class="wrapper-text-home">
                <div id="wrapper-first-row">
                    <div id="first-row">
                        <ul>
                            {#each technology as technology, i}
                                <li
                                    id={i}
                                    class={nestedSelected[i] === i
                                        ? "nested-link active"
                                        : "nested-link"}
                                    on:click={handleNestedNavigation}
                                >
                                    <a
                                        id={i}
                                        href={technology.url}
                                        alt="en route pour {technology.name}"
                                        >{technology.name}</a
                                    >
                                </li>
                            {/each}
                        </ul>
                    </div>
                </div>
                <div id="wrapper-remaining-row">
                    <p>THE TERMINOLOGY ...</p>
                    <div id="second-row">{nestedSelected.name}</div>

                    <div id="third-row">
                        {nestedSelected.description}
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<style>
    #technology {
        background: url("/assets/technology/background-technology-desktop.jpg");
        top: 0;
        z-index: 1;
        min-height: calc(100 * var(--vh));
        height: calc(100 * var(--vh));
        width: 100%;
        background-size: cover;
        background-repeat: no-repeat;
        background-position-x: center;
        background-position-y: center;
        display: flex;
        display: -webkit-box;
        display: -ms-flexbox;
        justify-content: center;
        align-items: flex-end;
        -webkit-box-pack: center;
        -ms-flex-pack: center;
        -webkit-box-align: end;
        -ms-flex-align: end;
    }
    #wrapper-grid-technology {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: calc(100 * var(--vh) - 200px);
        margin-top: auto;
        width: 90%;
        margin-left: auto;
    }
    #header-technology {
        display: flex;
        width: 100%;
        justify-content: flex-start;
        align-items: center;
        padding-left: 10%;
    }
    #grid-technology {
        width: 100%;
        height: calc(100% - 22px);
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -ms-flex-pack: distribute;
        justify-content: space-evenly;
        align-items: center;
        margin: auto;
        color: white;
        flex-direction: row-reverse;
    }

    h1 {
        color: white;
        font-family: "Barlow";
        font-size: 18px;
        letter-spacing: 2px;
    }
    h1 span {
        margin-right: 8px;
        color: #4a5667;
    }
    .wrapper-text-home {
        width: 60%;
        height: 60%;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: flex-start;
        color: white;
        align-self: inherit;
    }
    .wrapper-image-grid {
        display: flex;
        justify-content: flex-end;
        align-items: center;
        height: 100%;
        width: 40%;
    }
    .wrapper-image-grid img {
        height: auto;
        width: 100%;
    }
    #wrapper-first-row {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        padding: 24px;
        margin-bottom: 0;
    }
    #wrapper-remaining-row {
        display: flex;
        flex-direction: column;
        height: 100%;
        justify-content: flex-start;
        align-items: center;
        width: max-content;
        margin: auto;
        margin-left: 0;
        padding: 24px;
    }
    #wrapper-remaining-row p {
        margin-right: auto;
        margin-bottom: 8px;
        font-family: "Barlow";
        font-size: 0.8rem;
        color: rgba(255, 255, 255, 0.7);
    }
    #first-row {
        font-family: "Barlow";
        font-size: 1rem;
        letter-spacing: normal;
        width: 100%;
        display: flex;
        justify-content: flex-start;
        height: 100%;
    }
    #first-row ul {
        display: flex;
        flex-direction: row;
        font-size: 10px;
        font-family: "Barlow";
        list-style: none;
        justify-content: space-between;
        align-items: flex-start;
        width: 100%;
        height: 100%;
        flex-direction: column;
    }

    #first-row ul li {
        width: max-content;
        height: max-content;
        padding: 8px;
        margin-bottom: 0;
    }

    #first-row ul li a {
        display: flex;
        width: 48px;
        height: 48px;
        border: 1px solid white;
        border-radius: 50%;
        margin-bottom: 0;
        justify-content: center;
        align-items: center;
        font-family: "Bellefair";
        font-size: 1.5rem;
    }

    ul li.nested-link a {
        background-color: black;
        color: white;
    }

    ul li.nested-link:hover a {
        background-color: white;
        color: black;
    }

    ul li.nested-link.active a {
        background-color: white;
        color: black;
    }

    #second-row {
        font-family: "Bellefair";
        font-size: 3.5rem;
        width: 100%;
        white-space: nowrap;
    }
    #third-row {
        font-family: "Barlow";
        font-size: 1rem;
        line-height: 2;
        letter-spacing: 0.5px;
        width: 100%;
        color: rgba(255, 255, 255, 0.7);
        margin-top: auto;
    }
    @media (max-width: 70rem) {
        #wrapper-grid-technology {
            width: 100%;
        }
        #second-row {
            font-size: 2.5rem;
        }
        #third-row {
            line-height: 1.5;
        }
    }

    @media (max-width: 50rem) {
        #wrapper-grid-technology {
            height: calc(100 * var(--vh) - 100px);
            width: 100%;
        }
        #header-technology {
            margin-bottom: 20px;
            padding-left: 10%;
        }
        #grid-technology {
            flex-direction: column;
            align-items: center;
            height: 100%;
        }
        .wrapper-text-home * {
            margin-bottom: 0;
        }

        .wrapper-text-home {
            align-items: center;
            text-align: center;
            width: 100%;
            height: 50%;
            flex-direction: column;
        }
        .wrapper-image-grid {
            width: 100%;
            height: auto;
            align-items: flex-end;
        }
        .wrapper-image-grid img {
            width: 100%;
        }
        #wrapper-first-row {
            padding: 4px;
            width: auto;
            height: auto;
        }
        #wrapper-remaining-row {
            width: 100%;
            text-align: center;
            padding: 8px;
        }
        #wrapper-remaining-row p {
            text-align: center;
            margin-inline: auto;
            margin-block: 10px;
        }
        #first-row {
            width: 100%;
        }
        #first-row ul {
            justify-content: center;
            flex-direction: row;
        }
        #first-row ul li {
            padding: 12px;
        }
        #second-row {
            font-family: "Bellefair";
            font-size: 2.5rem;
            letter-spacing: 0.2rem;
        }
        #third-row {
            margin-bottom: 20px;
        }
    }
    @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
        #wrapper-grid-technology {
            height: calc(100 * var(--vh) - 100px);
        }
        #header-technology {
            margin-bottom: 20px;
        }
        #grid-technology {
            flex-direction: column;
        }
        .wrapper-text-home {
            align-items: center;
            justify-content: space-between;
            text-align: center;
            width: 100%;
            flex-direction: column;
        }
        .wrapper-image-grid {
            width: 100%;
            height: auto;
        }
        .wrapper-image-grid img {
            width: 100%;
            height: auto;
        }
        #wrapper-first-row {
            padding: 4px;
            width: 50%;
            height: auto;
        }
        #wrapper-remaining-row {
            width: 70%;
            text-align: center;
            padding: 8px;
            justify-content: center;
            margin: auto;
        }
        #wrapper-remaining-row p {
            text-align: center;
            margin-inline: auto;
            margin-block: 10px;
        }
        #first-row {
            width: 100%;
            margin-bottom: auto;
            height: auto;
        }
        #first-row ul {
            justify-content: center;
            flex-direction: row;
        }
        #first-row ul li {
            margin: 12px;
        }
        #second-row {
            font-family: "Bellefair";
            font-size: 2.5rem;
            letter-spacing: 0.2rem;
        }
        #third-row {
            margin: auto;
            font-size: 1.2rem;
            line-height: 1.8rem;
        }
    }
    @media only screen and (max-width: 520px) {
        #header-technology {
            padding-left: 0;
        }
        #header-technology h1 {
            font-size: 12px;
            margin: auto;
            padding-left: 0;
        }

        #grid-technology {
            height: 100%;
        }
        #wrapper-first-row {
            margin-block: 5%;
        }
        #first-row ul li {
            margin: 4px;
            padding-block: 4px;
        }
        #first-row ul li a {
            width: 36px;
            height: 36px;
        }
        #wrapper-remaining-row {
            justify-content: flex-start;
        }
        #wrapper-remaining-row p {
            text-align: center;
            margin-inline: auto;
            font-size: 0.7rem;
            margin-block: 10px;
        }
        #second-row {
            font-size: 1.5rem;
            margin-top: 4px;
        }
        #third-row {
            width: 100%;
            font-size: 18px;
            margin-top: 5%;
            margin-bottom: 0;
        }
        .wrapper-image-grid {
            width: 100%;
            height: auto;
            margin-bottom: auto;
        }
        .wrapper-text-home {
            justify-content: space-around;
            margin-bottom: auto;
            height: inherit;
        }
        .wrapper-text-home * {
            margin-bottom: 0;
        }
    }
    @media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
        .wrapper-image-grid {
            width: 100%;
            height: auto;
            margin-bottom: auto;
        }
        #third-row {
            font-size: 14px;
        }
    }
    @media only screen and (max-device-width: 320px) {
        #wrapper-first-row {
            margin-block: 0;
        }
        #third-row {
            font-size: 12px;
        }
    }
</style>
