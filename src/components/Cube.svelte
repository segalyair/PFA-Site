<script>
    import { onMount } from "svelte";
    import Intro from "./home/Intro.svelte";
    import Empty from "./home/Empty.svelte";
    import Welcome from "./home/Welcome.svelte";
    let cube;
    function rotateCubeFace(to) {
        if (to == getComputedStyle(cube).getPropertyValue("--to")) return;
        const animCls = cube.classList[cube.classList.length - 1];
        if (animCls == "animation") {
            return;
        }
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
        <div class="cube__face cube__face--back"><Empty showImg={false} /></div>
        <div
            class="cube__face cube__face--back-reverse"
            on:click={() =>
                rotateCubeFace(
                    "translateZ(300px) rotateX(355deg) rotateY(15deg)"
                )}
        >
            <Empty />
        </div>
        <div class="cube__face cube__face--right"><Welcome /></div>
        <div
            class="cube__face cube__face--right-reverse"
            on:click={() =>
                rotateCubeFace(
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
            on:click={() =>
                rotateCubeFace(
                    "translateZ(300px) rotateX(280deg) rotateY(0deg)"
                )}
        >
            <Empty />
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
        cursor: pointer;
        -webkit-font-smoothing: subpixel-antialiased;
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
    .cube__face:hover {
        border: 1px solid yellow;
    }
    .cube__face--right {
        transform: rotateY(90deg) translateZ(calc(var(--size) / 2));
    }
    .cube__face--right-reverse {
        transform: rotateY(270deg) translateZ(calc(var(--size) / -2));
    }
    .cube__face--back {
        transform: rotateY(180deg) translateZ(calc(var(--size) / 2));
    }
    .cube__face--back-reverse {
        transform: rotateY(0deg) translateZ(calc(var(--size) / -2));
    }
    .cube__face--bottom {
        transform: rotateX(-90deg) translateZ(calc(var(--size) / 2));
    }
    .cube__face--bottom-reverse {
        transform: rotateX(-270deg) translateZ(calc(var(--size) / -2));
    }
    @keyframes rotate {
        to {
            transform: var(--to);
        }
    }
</style>
