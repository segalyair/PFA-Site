<script>
    export let showImg = false;
</script>

<div class="container">
    {#if showImg}
        <img width="100" src="./img/finger-pointer.png" alt="Finger pointer" />
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
