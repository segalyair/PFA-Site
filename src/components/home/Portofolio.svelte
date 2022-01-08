<script>
    function downloadPortofolio() {
        var link = document.createElement("a");
        link.href = "./Resume.pdf";
        link.download = "Yair_Segal_CV.pdf";
        link.dispatchEvent(new MouseEvent("click"));
    }
</script>

<div class="container">
    <div class="content">
        <h2>Portofolio</h2>
        <div class="list">
            <a
                class="item"
                href="https://developer.signicat.com/"
                target="_blank">Signicat Developer Portal</a
            >
            <a class="item" href="https://creante-ro.web.app/" target="_blank">
                Receivables Market</a
            >
        </div>
        <h2 style="margin-top:1rem">Resume / CV</h2>
        <button on:click={downloadPortofolio}>Download</button>
    </div>
</div>

<style>
    .content {
        padding: 2rem;
    }
    .list {
        display: flex;
        flex-direction: column;
    }
    .item {
        position: relative;
        padding: 1rem 0;
        color: lightyellow;
        transition: all 200ms;
    }
    .item::after {
        position: absolute;
        bottom: 0;
        left: 0;
        content: "";
        width: 0;
        height: 2px;
        background: orange;
        transition: all 200ms;
    }
    .item:hover {
        color: orange;
    }
    .item:hover::after {
        width: 100%;
    }
    button {
        background: lightyellow;
        border: 2px solid transparent;
        border-radius: 0;
        padding: 0.5rem 1rem;
        cursor: pointer;
        transition: all 200ms;
    }
    button:hover {
        background: orange;
        border: 2px solid orange;
        color: #444;
    }
</style>
