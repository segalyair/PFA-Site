<script>
    export let background = "#444",
        showImg = true;
</script>

<div class="container" style={`background:${background}`}>
    {#if showImg}
        <img width="100" src="./finger-pointer.png" alt="Finger pointer" />
    {/if}
</div>

<style>
    .container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
    }
</style>
