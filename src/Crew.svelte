<script>
    import { onMount } from "svelte";
    import { crew } from "./data.json";

    const allLinks = document.getElementsByClassName("nested-link");

    $: innerWidth = 0;
    const allWrapperTextHome =
        document.getElementsByClassName("wrapper-text-home");
    onMount(() => {
        let wrapperTextHome = allWrapperTextHome[0];
        const firstElement = wrapperTextHome.firstChild;
        const lastElement = wrapperTextHome.lastChild;

        if (innerWidth <= 520) {
            console.log("largeur d'écran inférieur ou égale à 320", innerWidth);
            console.log(wrapperTextHome);
            wrapperTextHome.insertBefore(lastElement, firstElement);
        }

        if (allLinks.length > 0) {
            allLinks[0].classList.add("active");
        }
        for (let i = 0; i < crew.length; i++) {
            allLinks[i].firstElementChild.textContent = "";
            if (crew[i].url === window.location.hash) {
                selected = crew[i];
            }
        }
    });

    $: nestedSelected = crew[0];

    function handleNestedNavigation(event) {
        event.preventDefault();
        nestedSelected = crew[event.srcElement.id];

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

<svelte:window bind:innerWidth />

<div id="crew">
    <div id="wrapper-grid-crew">
        <div id="header-crew">
            <h1><span>02</span>MEET YOUR CREW</h1>
        </div>

        <div id="grid-crew">
            <div class="wrapper-text-home">
                <div id="second-row">{nestedSelected.role}</div>

                <div id="third-row">
                    {nestedSelected.name}
                </div>
                <div id="fourth-row">
                    {nestedSelected.bio}
                </div>
                <div id="first-row">
                    <ul>
                        {#each crew as crew, i}
                            <li
                                id={i}
                                class={nestedSelected[i] === i
                                    ? "nested-link active"
                                    : "nested-link"}
                                on:click={handleNestedNavigation}
                            >
                                <a
                                    id={i}
                                    href={crew.url}
                                    alt="en route pour {crew.name}"
                                    >{crew.name}</a
                                >
                            </li>
                        {/each}
                    </ul>
                </div>
            </div>
            <div class="wrapper-image-grid">
                <img src={nestedSelected.images.webp} alt="moon" />
                <hr id="separator" />
            </div>
        </div>
    </div>
</div>

<style>
    #crew {
        background: url("/assets/crew/background-crew-desktop.jpg");
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
    #wrapper-grid-crew {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: auto;
        width: 100%;
    }
    #header-crew {
        display: flex;
        width: 80%;
        justify-content: flex-start;
        align-items: center;
    }
    #grid-crew {
        width: 80%;
        height: auto;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -ms-flex-pack: distribute;
        justify-content: space-evenly;
        align-items: center;
        margin: auto;
        height: calc(100 * var(--vh) - 200px);
        color: white;
        position: inherit;
    }
    #grid-crew > * {
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

    hr#separator {
        display: none;
        width: 80%;
        border: 1px solid rgba(255, 255, 255, 0.1);
        margin-bottom: 30px;
    }
    #first-row {
        font-family: "Barlow";
        font-size: 1rem;
        letter-spacing: normal;
        width: 30%;
        display: flex;
        justify-content: flex-start;
        margin-block: 50px;
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
        padding: 8px;
        margin-bottom: 0;
    }

    #first-row ul li a {
        display: flex;
        width: 12px;
        height: 12px;
        border-radius: 50%;
        margin-bottom: 0;
    }

    ul li.nested-link a {
        background-color: #4a5667;
    }

    ul li.nested-link:hover a {
        background-color: white;
    }

    ul li.nested-link.active a {
        background-color: white;
    }

    #second-row {
        font-family: "Bellefair";
        font-size: 2rem;
        letter-spacing: 0.5px;
        margin-top: auto;
        width: 80%;
        color: rgba(255, 255, 255, 0.7);
    }
    #third-row {
        font-family: "Bellefair";
        font-size: 3rem;
        letter-spacing: 0.2rem;
    }
    #fourth-row {
        font-family: "Barlow";
        font-size: 0.8rem;
        line-height: 1.2rem;
        letter-spacing: 0.5px;
        margin-bottom: auto;
        width: 80%;
        color: rgba(255, 255, 255, 0.7);
    }

    #wrapper-travel-info {
        display: flex;
        margin-bottom: 0;
    }
    .wrapper-image-grid {
        display: flex;
        justify-content: center;
        align-items: flex-end;
        width: 100%;
        height: inherit;
    }
    .wrapper-image-grid img {
        height: inherit;
        width: auto;
        object-fit: contain;
    }
    @media (max-width: 70rem) {
        #first-row {
            width: 200px;
        }
        #grid-crew {
            width: 90%;
        }
    }
    @media (max-width: 50rem) {
        #wrapper-grid-crew {
            height: calc(100 * var(--vh) - 100px);
        }
        #header-crew {
            margin-bottom: 20px;
        }
        #grid-crew {
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
        .wrapper-image-grid {
            align-items: flex-end;
        }
        .wrapper-image-grid img {
            width: auto;
            height: 250px;
        }
        #first-row {
            width: 50%;
            margin-block: 25px;
        }
        #first-row ul {
            justify-content: center;
        }
        #first-row ul li {
            margin: 12px;
        }
        #second-row {
            font-family: "Bellefair";
            font-size: 1.2rem;
            letter-spacing: 0.2rem;
        }
        #third-row {
            margin-bottom: 20px;
            font-size: 2rem;
        }

        #fourth-row {
            margin-bottom: 0;
        }
    }
    @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
        #wrapper-grid-crew {
            height: calc(100 * var(--vh) - 100px);
        }
        #header-crew {
            margin-bottom: 20px;
        }
        #grid-crew {
            margin-bottom: 0;
            flex-direction: column;
        }
        .wrapper-text-home {
            align-items: center;
            justify-content: space-between;
            text-align: center;
        }
        .wrapper-image-grid {
            align-items: center;
        }
        .wrapper-image-grid img {
            width: auto;
            height: 500px;
            margin-top: auto;
        }
        #first-row {
            width: 200px;
        }
        #first-row ul {
            justify-content: center;
        }
        #first-row ul li {
            margin: 12px;
        }
        #second-row {
            font-family: "Bellefair";
            font-size: 1.2rem;
            letter-spacing: 0.2rem;
            margin-top: 0;
        }
        #third-row {
            margin-bottom: 20px;
            font-size: 2rem;
        }
        #fourth-row {
            margin-bottom: 0;
            font-size: 1rem;
            line-height: 2rem;
        }
    }
    @media only screen and (max-width: 520px) {
        #header-crew h1 {
            font-size: 12px;
            margin: auto;
        }
        .wrapper-image-grid {
            flex-direction: column;
            align-items: center;
        }
        .wrapper-image-grid img {
            width: auto;
            height: 175px;
            margin: 0;
        }
        #grid-crew {
            height: 100%;
            flex-direction: column-reverse;
            width: 90%;
            margin-bottom: 50px;
        }
        hr#separator {
            display: flex;
        }
        #first-row {
            margin-block: 0;
        }
        #first-row ul li {
            margin: 4px;
            padding-block: 4px;
        }
        #second-row {
            font-size: 0.7rem;
        }
        #third-row {
            width: 100%;
            font-size: 18px;
            margin: auto;
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
    }
    @media only screen and (max-width: 320px) {
        #grid-crew {
            margin-bottom: 12px;
        }
        #fourth-row {
            font-size: 0.7rem;
        }
    }
</style>
