<script>
    import { onMount } from "svelte";
    import Intro from "./home/Intro.svelte";
    import Empty from "./home/Empty.svelte";
    import Welcome from "./home/Welcome.svelte";
    import Contact from "./home/Contact.svelte";
    import Portofolio from "./home/Portofolio.svelte";
    import { hideInfo } from "../store.js";
    let cube,
        currentFace = "right-reverse";
    function rotateCubeFace(face, to) {
        if (to == getComputedStyle(cube).getPropertyValue("--to")) return;
        const animCls = cube.classList[cube.classList.length - 1];
        if (animCls == "animation") {
            return;
        }
        hideInfo.set(true);
        currentFace = face;
        cube.style.setProperty("--to", to);
        cube.classList.add("animation");
    }
    onMount(() => {
        cube.classList.add("animation");
        cube.addEventListener("animationend", () => {
            cube.style.setProperty("--delay", "0s");
            cube.style.setProperty("--speed", "1s");
            cube.style.setProperty(
                "--tstate",
                getComputedStyle(cube).getPropertyValue("--to")
            );
            cube.classList.remove("animation");
        });
    });
</script>

<div class="scene">
    <div class="cube" bind:this={cube}>
        <div class="cube__face cube__face--back"><Empty /></div>
        <div
            class="cube__face cube__face--back-reverse"
            class:active={currentFace == "back-reverse"}
            on:click={() =>
                rotateCubeFace(
                    "back-reverse",
                    "translateZ(300px) rotateX(355deg) rotateY(15deg)"
                )}
        >
            <Portofolio />
        </div>
        <div class="cube__face cube__face--right"><Welcome /></div>
        <div
            class="cube__face cube__face--right-reverse"
            class:active={currentFace == "right-reverse"}
            on:click={() =>
                rotateCubeFace(
                    "right-reverse",
                    "translateZ(300px) rotateX(355deg) rotateY(75deg)"
                )}
        >
            <Intro />
        </div>
        <div class="cube__face cube__face--bottom">
            <Empty showImg={false} />
        </div>
        <div
            class="cube__face cube__face--bottom-reverse"
            class:active={currentFace == "bottom-reverse"}
            on:click={() =>
                rotateCubeFace(
                    "bottom-reverse",
                    "translateZ(300px) rotateX(280deg) rotateY(0deg)"
                )}
        >
            <Contact />
        </div>
    </div>
</div>

<style>
    .scene {
        --size: 400px;
        width: var(--size);
        height: var(--size);
        perspective: calc(var(--size) * 3);
        user-select: none;
        -webkit-tap-highlight-color: transparent;
    }

    .cube {
        --speed: 2s;
        --delay: 1s;
        --tstate: translateZ(-100px) rotateX(345deg) rotateY(-110deg);
        --to: translateZ(300px) rotateX(355deg) rotateY(75deg);
        width: 100%;
        height: 100%;
        position: relative;
        transform-style: preserve-3d;
        transform: var(--tstate);
        -webkit-font-smoothing: subpixel-antialiased;
        -webkit-tap-highlight-color: transparent;
    }
    :global(.cube.animation) {
        cursor: wait;
        animation: rotate var(--speed) var(--delay) forwards;
    }

    .cube__face {
        position: absolute;
        width: var(--size);
        height: var(--size);
        border: 1px solid lightyellow;
    }
    .cube__face:hover:not(.active) {
        cursor: pointer;
        border: 1px solid orangered;
    }
    .cube__face.active {
        pointer-events: all;
        cursor: initial;
        border: 1px solid orange;
    }
    .cube__face--right {
        background: #444;
        transform: rotateY(90deg) translateZ(calc(var(--size) / 2));
    }
    .cube__face--right-reverse {
        background: linear-gradient(226deg, #444 93%, black 146%);
        transform: rotateY(270deg) translateZ(calc(var(--size) / -2));
    }
    .cube__face--back {
        background: #444;
        transform: rotateY(180deg) translateZ(calc(var(--size) / 2));
    }
    .cube__face--back-reverse {
        background: linear-gradient(138deg, #444 93%, black 146%);
        transform: rotateY(0deg) translateZ(calc(var(--size) / -2));
    }
    .cube__face--bottom {
        transform: rotateX(-90deg) translateZ(calc(var(--size) / 2));
    }
    .cube__face--bottom-reverse {
        background: linear-gradient(50deg, #444 93%, black 146%);
        transform: rotateX(-270deg) translateZ(calc(var(--size) / -2));
    }
    @keyframes rotate {
        to {
            transform: var(--to);
        }
    }
</style>
