<script>
    import Intro from "./home/Intro.svelte";
    import Welcome from "./home/Welcome.svelte";
</script>

<div class="scene">
    <div class="cube">
        <div class="cube__face cube__face--back"><Intro /></div>
        <div class="cube__face cube__face--back-reverse"><Intro /></div>
        <div class="cube__face cube__face--right"><Welcome /></div>
        <div class="cube__face cube__face--right-reverse"><Intro /></div>
        <div class="cube__face cube__face--bottom"><Intro /></div>
        <div class="cube__face cube__face--bottom-reverse"><Intro /></div>
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
        width: 100%;
        height: 100%;
        position: relative;
        transform-style: preserve-3d;
        transform: translateZ(-100px) rotateX(345deg) rotateY(-110deg);
        animation: rotate-start 2s 1s forwards;
    }

    .cube__face {
        position: absolute;
        width: var(--size);
        height: var(--size);
        border: 1px solid lightgray;
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
    @keyframes rotate-start {
        to {
            transform: translateZ(300px) rotateX(355deg) rotateY(75deg);
        }
    }
</style>
