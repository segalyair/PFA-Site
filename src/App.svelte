<script>
	import Cube from "./components/Cube.svelte";
	import { hideInfo } from "./store.js";
	import { fade } from "svelte/transition";
</script>

<main>
	{#if !$hideInfo}
		<div class="info" transition:fade>
			<img width="75" src="./img/finger-pointer.png" alt="help" />
			<span>Click on a face to rotate.</span>
		</div>
	{/if}
	<Cube />
</main>

<style>
	.info {
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 24px;
		position: fixed;
		top: 0;
		margin: 2rem auto auto auto;
		color: lightyellow;
		animation: hide;
	}
	main {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
	}
</style>
