<script>
</script>

<div id="homepage">
    <div id="grid-home">
        <div class="wrapper-text-home">
            <div id="first-row">SO, YOU WANT TO TRAVEL TO</div>
            <div id="second-row">SPACE</div>
            <div id="third-row">
                Let’s face it; if you want to go to space, you might as well
                genuinely go to outer space and not hover kind of on the edge of
                it. Well sit back, and relax because we’ll give you a truly out
                of this world experience!
            </div>
        </div>
        <div class="wrapper-explore-button">
            <button id="explore-space">EXPLORE</button>
        </div>
    </div>
</div>

<style>
    #homepage {
        background: url("/assets/home/background-home-desktop.jpg");
        top: 0;
        z-index: 1;
        min-height: 100vh;
        width: 100%;
        background-size: cover;
        background-repeat: no-repeat;
        background-position-x: center;
        background-position-y: center;
        display: flex;
        display: -webkit-box;
        display: -ms-flexbox;
        justify-content: flex-end;
        align-items: flex-end;
        -webkit-box-pack: end;
        -ms-flex-pack: end;
        -webkit-box-align: end;
        -ms-flex-align: end;
    }
    #grid-home {
        width: 100%;
        height: auto;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -ms-flex-pack: distribute;
        justify-content: space-around;
        margin-bottom: 100px;
    }

    .wrapper-text-home {
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
        color: rgba(255, 255, 255, 0.7);
    }
    #second-row {
        font-family: "Bellefair";
        font-size: 7rem;
        letter-spacing: 0.2rem;
        margin-top: 12px;
    }
    #third-row {
        font-family: "Barlow";
        font-size: 0.8rem;
        line-height: 1.2rem;
        letter-spacing: 0.5px;
        color: rgba(255, 255, 255, 0.7);
    }
    .wrapper-explore-button {
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
    @media (max-width: 50rem) {
        #homepage {
            justify-content: center;
            align-items: center;
            background: url("/assets/home/background-home-tablet.jpg");
            min-height: 100vh;
            width: 100%;
            background-size: cover;
            background-repeat: no-repeat;
            background-position-x: center;
            background-position-y: center;
            display: flex;
            justify-content: center;
            align-items: flex-end;
        }
        #grid-home {
            -webkit-box-orient: vertical;
            -webkit-box-direction: normal;
            -ms-flex-direction: column;
            flex-direction: column;
            -webkit-box-align: center;
            -ms-flex-align: center;
            align-items: center;
            -webkit-box-pack: center;
            -ms-flex-pack: center;
            justify-content: center;
            margin-bottom: 10px;
        }

        .wrapper-explore-button {
            margin: auto;
        }
        .wrapper-text-home {
            align-items: center;
            text-align: center;
            margin: auto;
        }

        #explore-space {
            width: 200px;
            height: 200px;
        }
        #explore-space::before {
            width: 200px;
            height: 200px;
        }
    }
    @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
        #homepage {
            justify-content: center;
        }
        #grid-home {
            grid-template-columns: auto;
            margin: auto;
            align-items: center;
            grid-row-gap: 100px;
            padding: 50px;
        }
        .wrapper-explore-button {
            margin: auto;
        }
        .wrapper-text-home {
            align-items: center;
            text-align: center;
        }
        #first-row {
            font-size: 1.5rem;
        }
        #second-row {
            font-size: 9rem;
        }
    }
    @media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
        #homepage {
            background: url("/assets/home/background-home-mobile.jpg");
            height: calc(100vh - 100px);
            width: 100%;
            background-size: cover;
            background-repeat: no-repeat;
            background-position-x: center;
            background-position-y: center;
            display: flex;
            justify-content: center;
            align-items: flex-end;
            position: absolute;
            z-index: 2;
            bottom: env(safe-area-inset-bottom);
        }
        #grid-home {
            grid-row-gap: 75px;
            height: calc(100vh - 100px);
        }
        .wrapper-text-home {
            margin: auto;
        }
        .wrapper-text-home * {
            margin: 0;
        }
        #first-row {
            font-size: 0.8rem;
        }
        #second-row {
            font-size: 5rem;
        }
        #third-row {
            font-size: 0.7rem;
        }
        .wrapper-explore-button {
            width: auto;
            height: auto;
        }
        #explore-space {
            width: 150px;
            height: 150px;
            font-size: 1.5rem;
        }
        #explore-space::before {
            display: none;
        }
    }
</style>
