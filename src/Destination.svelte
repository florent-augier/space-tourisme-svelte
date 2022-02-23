<script>
    import { onMount } from "svelte";
    import { destinations } from "./data.json";

    const allLinks = document.getElementsByClassName("nested-link");

    $: nestedSelected = destinations[0];

    onMount(() => {
        if (allLinks.length > 0) {
            allLinks[0].classList.add("active");
        }
        for (let i = 0; i < destinations.length; i++) {
            if (destinations[i].url === window.location.hash) {
                selected = destinations[i];
            }
        }
    });

    function handleNestedNavigation(event) {
        event.preventDefault();
        nestedSelected = destinations[event.srcElement.id];

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

<div id="destination">
    <div id="wrapper-grid-destination">
        <div id="header-destination">
            <h1><span>01</span>PICK YOUR DESTINATION</h1>
        </div>

        <div id="grid-destination">
            <div class="wrapper-image-grid">
                <img src={nestedSelected.images.webp} alt="moon" />
            </div>
            <div class="wrapper-text-home">
                <div id="first-row">
                    <ul>
                        {#each destinations as destination, i}
                            <li
                                id={i}
                                class={nestedSelected[i] === i
                                    ? "nested-link active"
                                    : "nested-link"}
                                on:click={handleNestedNavigation}
                            >
                                <a
                                    id={i}
                                    href={destination.url}
                                    alt="en route pour {destination.name}"
                                    >{destination.name}</a
                                >
                            </li>
                        {/each}
                    </ul>
                </div>
                <div id="second-row">{nestedSelected.name}</div>

                <div id="third-row">
                    {nestedSelected.description}
                </div>
                <hr id="separator" />
                <div id="fourth-row">
                    <div id="wrapper-travel-info">
                        <div>
                            <p class="data-header">AVG. DISTANCE</p>
                            <p class="data-result">{nestedSelected.distance}</p>
                        </div>
                        <div>
                            <p class="data-header">EST. TRAVEL TIME</p>
                            <p class="data-result">{nestedSelected.travel}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<style>
    #destination {
        background: url("/assets/destination/background-destination-desktop.jpg");
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
    #wrapper-grid-destination {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: calc(100 * var(--vh) - 200px);
        margin-top: auto;
        width: 90%;
    }
    #header-destination {
        display: flex;
        width: 100%;
        justify-content: flex-start;
        align-items: center;
    }
    #grid-destination {
        width: 100%;
        height: 100%;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -ms-flex-pack: distribute;
        justify-content: space-evenly;
        align-items: center;
        margin: auto;
        color: white;
    }
    #grid-destination > * {
        width: 100%;
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
        width: min-content;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        color: white;
        align-self: inherit;
    }
    .wrapper-text-home * {
        margin-bottom: 10px;
    }
    #first-row {
        font-family: "Barlow";
        font-size: 1rem;
        letter-spacing: normal;
        width: 40%;
        display: flex;
        justify-content: flex-start;
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
    }
    #first-row ul li {
        width: max-content;
        height: max-content;
    }

    #first-row ul li a {
        font-family: "Barlow";
        font-size: 12px;
        color: white;
        text-decoration: none;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    #first-row ul li,
    #first-row ul li a {
        color: white;
    }

    ul li.nested-link:hover {
        height: calc(100% - 2px);
        border-bottom: 2px solid lightslategray;
        margin-bottom: -2px;
    }

    ul li.nested-link.active {
        height: calc(100% - 2px);
        border-bottom: 2px solid white;
        margin-bottom: -2px;
    }

    #second-row {
        font-family: "Bellefair";
        font-size: 4rem;
        letter-spacing: 0.2rem;
    }
    #third-row {
        font-family: "Barlow";
        font-size: 0.8rem;
        line-height: 1.2rem;
        letter-spacing: 0.5px;
        margin-bottom: auto;
        width: 80%;
        color: rgba(255, 255, 255, 0.7);
    }
    hr#separator {
        width: 80%;
        border: 1px solid rgba(255, 255, 255, 0.1);
        margin-bottom: 30px;
    }
    #wrapper-travel-info {
        display: flex;
        margin-bottom: 0;
    }
    #wrapper-travel-info div {
        display: flex;
        flex-direction: column;
    }
    #wrapper-travel-info div,
    #wrapper-travel-info p {
        text-align: start;
        padding: 8px;
    }
    .data-header {
        font-family: "Barlow";
        font-size: 12px;
        color: rgba(255, 255, 255, 0.7);
        text-transform: uppercase;
    }
    .data-result {
        font-family: "Bellefair";
        font-size: 1.5rem;
        text-transform: uppercase;
        padding-right: 50px;
    }

    .wrapper-image-grid {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .wrapper-image-grid img {
        width: 300px;
        height: 300px;
        margin: auto;
    }
    @media (max-width: 50rem) {
        #wrapper-grid-destination {
            height: calc(100 * var(--vh) - 100px);
        }
        #header-destination {
            margin-bottom: 20px;
        }
        #grid-destination {
            flex-direction: column;
            align-items: center;
            height: 100%;
        }
        .wrapper-text-home * {
            margin-bottom: 4px;
        }

        .wrapper-text-home {
            align-items: center;
            text-align: center;
        }
        .wrapper-image-grid img {
            width: 200px;
            height: 200px;
            margin: auto;
        }
        #first-row {
            width: 100%;
        }
        #first-row ul {
            justify-content: center;
        }
        #first-row ul li {
            margin: 12px;
        }
        #second-row {
            font-family: "Bellefair";
            font-size: 3.5rem;
            letter-spacing: 0.2rem;
        }
        #third-row {
            margin-bottom: 20px;
        }
        hr#separator {
            margin-bottom: 10px;
        }
        #fourth-row {
            margin-bottom: 0;
        }
    }
    @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
        #wrapper-grid-destination {
            height: calc(100 * var(--vh) - 100px);
        }
        #header-destination {
            margin-bottom: 20px;
        }
        #grid-destination {
            flex-direction: column;
        }
        .wrapper-text-home {
            align-items: center;
            justify-content: space-between;
            margin-bottom: 24px;
            text-align: center;
        }
        .wrapper-image-grid img {
            width: 300px;
            height: 300px;
            margin: auto;
        }
        #first-row {
            width: 100%;
        }
        #first-row ul {
            justify-content: center;
        }
        #first-row ul li {
            margin: 12px;
        }
        #second-row {
            font-family: "Bellefair";
            font-size: 3.5rem;
            letter-spacing: 0.2rem;
        }
        #third-row {
            margin-bottom: 20px;
            font-size: 1.2rem;
            line-height: 1.8rem;
        }
        #fourth-row {
            margin-bottom: 0;
        }
    }
    @media only screen and (max-width: 520px) {
        #header-destination h1 {
            font-size: 12px;
            margin: auto;
        }
        .wrapper-image-grid img {
            width: 200px;
            height: 200px;
        }
        #grid-destination {
            height: 100%;
        }
        #first-row ul li {
            margin: 4px;
            padding-block: 4px;
        }
        #second-row {
            font-size: 2.5rem;
        }
        #third-row {
            width: 100%;
            font-size: 12px;
        }
        .wrapper-text-home {
            justify-content: space-around;
        }
        .wrapper-text-home * {
            margin-bottom: 0;
        }
        #separator {
            margin-bottom: 8px;
        }
        #wrapper-travel-info {
            flex-direction: column;
            text-align: center;
        }
        #wrapper-travel-info div,
        #wrapper-travel-info p {
            text-align: start;
            padding: 4px;
            text-align: center;
        }
        .data-header {
            font-size: 12px;
        }
        .data-result {
            font-size: 2rem;
        }
    }
    @media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
        hr#separator {
            margin-bottom: 8px;
        }
    }
    @media only screen and (max-device-width: 320px) {
        .wrapper-image-grid img {
            width: 120px;
            height: 120px;
        }
        hr#separator {
            margin-bottom: 8px;
        }
        .data-header {
            font-size: 8px;
        }
        .data-result {
            font-size: 1rem;
        }
    }
</style>
