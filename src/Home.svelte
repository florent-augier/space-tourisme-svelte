<script>
</script>

<div id="homepage">
    <div class="wrapper-text-home">
        <div id="first-row">SO, YOU WANT TO TRAVEL TO</div>
        <div id="second-row">SPACE</div>
        <div id="third-row">
            Let’s face it; if you want to go to space, you might as well
            genuinely go to outer space and not hover kind of on the edge of it.
            Well sit back, and relax because we’ll give you a truly out of this
            world experience!
        </div>
    </div>
    <div class="wrapper-explore-button">
        <button id="explore-space">EXPLORE</button>
    </div>
</div>

<style>
    #homepage {
        background: url("/assets/home/background-home-desktop.jpg");
        top: 0;
        z-index: 1;
        min-height: 100vh;
        width: 100%;
        min-height: 100vh;
        background-size: cover;
        background-repeat: no-repeat;
        background-position-x: center;
        background-position-y: center;
    }
    .wrapper-text-home {
        position: absolute;
        margin-top: 30%;
        margin-left: 10%;
        width: min-content;
        height: auto;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        color: white;
    }
    .wrapper-text-home * {
        margin: 10px;
    }
    #first-row {
        font-family: "Barlow";
        font-size: 1rem;
        letter-spacing: 0.2rem;
    }
    #second-row {
        font-family: "Bellefair";
        font-size: 7rem;
        letter-spacing: 0.2rem;
    }
    #third-row {
        font-family: "Barlow";
        font-size: 0.8rem;
        line-height: 1.2rem;
        letter-spacing: 0.5px;
    }
    .wrapper-explore-button {
        position: absolute;
        margin-top: 27%;
        margin-left: 60%;
        width: 300px;
        height: 300px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    #explore-space {
        width: 250px;
        height: 250px;
        background-color: white;
        margin: auto;
        border-radius: 50%;
        position: relative;
        font-family: "Bellefair";
        font-size: 2rem;
        color: black;
    }
    #explore-space::before {
        content: "";
        display: block;
        position: absolute;
        width: 250px;
        height: 250px;
        left: 0;
        top: 0;
        border-radius: 50%;
        background-color: rgba(255, 255, 255, 0.1);
        /* animation: grow 0.7s;
        -webkit-animation: grow 0.7s; */
        transition-property: transform, opacity;
        transition-duration: 0.7s;
        -webkit-transition-property: transform, opacity;
        -webkit-transition-duration: 0.7s;
        -o-transition-property: transform, opacity;
        -o-transition-duration: 0.7s;
        -moz-transition-property: transform, opacity;
        -moz-transition-duration: 0.7s;
        opacity: 0;
    }
    #explore-space:hover::before {
        transform: scale(1.5);
        opacity: 1;
    }
</style>
