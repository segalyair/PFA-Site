<script>
    import { onMount } from "svelte";
    import Intro from "./home/Intro.svelte";
    import Empty from "./home/Empty.svelte";
    import Welcome from "./home/Welcome.svelte";
    let cube,
        isAnimating = true;
    function rotateCubeFace(to, t) {
        const cls = cube.classList[cube.classList.length - 1];
        if (cls == to) return;
        if (cube.classList.length > 2) {
            cube.classList.remove(cls);
        }
        isAnimating = true;
        cube.classList.add(to);
        setTimeout(() => {
            cube.style.setProperty("--tstate", t);
            isAnimating = false;
        }, 2000);
    }
    onMount(() => {
        setTimeout(() => {
            isAnimating = false;
        }, 3000);
    });
</script>

<div class="scene">
    <div class="cube" bind:this={cube}>
        <div class="cube__face cube__face--back"><Empty /></div>
        <div
            class="cube__face cube__face--back-reverse"
            on:click={() =>
                !isAnimating &&
                rotateCubeFace(
                    "rotate-back-reverse",
                    "translateZ(300px) rotateX(355deg) rotateY(15deg)"
                )}
        >
            <Empty />
        </div>
        <div class="cube__face cube__face--right"><Welcome /></div>
        <div
            class="cube__face cube__face--right-reverse"
            on:click={() =>
                !isAnimating &&
                rotateCubeFace(
                    "rotate-right-reverse",
                    "translateZ(300px) rotateX(355deg) rotateY(75deg)"
                )}
        >
            <Intro />
        </div>
        <div class="cube__face cube__face--bottom"><Empty /></div>
        <div
            class="cube__face cube__face--bottom-reverse"
            on:click={() =>
                !isAnimating &&
                rotateCubeFace(
                    "rotate-bottom-reverse",
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
    }

    .cube {
        --tstate: translateZ(300px) rotateX(355deg) rotateY(75deg);
        width: 100%;
        height: 100%;
        position: relative;
        transform-style: preserve-3d;
        transform: translateZ(-100px) rotateX(345deg) rotateY(-110deg);
        animation: rotate-right-reverse 2s 1s forwards;
    }

    .cube__face {
        position: absolute;
        width: var(--size);
        height: var(--size);
        border: 1px solid lightyellow;
    }
    .cube__face:hover {
        border: 1px solid yellow;
        cursor: pointer;
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
    :global(.cube.rotate-right-reverse) {
        transform: var(--tstate);
        animation: rotate-right-reverse 2s forwards;
    }
    @keyframes rotate-right-reverse {
        to {
            transform: translateZ(300px) rotateX(355deg) rotateY(75deg);
        }
    }
    :global(.cube.rotate-back-reverse) {
        transform: var(--tstate);
        animation: rotate-back-reverse 2s forwards;
    }
    @keyframes rotate-back-reverse {
        to {
            transform: translateZ(300px) rotateX(355deg) rotateY(15deg);
        }
    }
    :global(.cube.rotate-bottom-reverse) {
        transform: var(--tstate);
        animation: rotate-bottom-reverse 2s forwards;
    }
    @keyframes rotate-bottom-reverse {
        to {
            transform: translateZ(300px) rotateX(280deg) rotateY(0deg);
        }
    }
</style>
