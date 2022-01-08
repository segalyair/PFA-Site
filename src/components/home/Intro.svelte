<div class="container">
    <div class="content">
        <div class="title">
            <div>
                <h2>About</h2>
                <p>Over 4 years experience in Web Development.</p>
            </div>

            <img src="./img/profile.jpg" alt="profile" width="100" />
        </div>

        <p>Multiple projects delivered for several companies:</p>
        <div class="companies">
            <img width="100" src="./img/ubisoft.svg" alt="Ubisoft" />
            <img width="75" src="./img/signicat.svg" alt="Signicat" />
            <img width="150" src="./img/swarco.svg" alt="Swarco" />
            <img width="175" src="./img/transperfect.svg" alt="Transperfect" />
            <img
                width="100"
                src="./img/senior_software.png"
                alt="Senior Software"
            />
        </div>
    </div>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
    }
    .title {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 1rem;
    }
    .title h2 {
        align-self: flex-start;
    }
    .title img {
        margin-left: 1rem;
        border-radius: 50%;
    }
    .companies {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-evenly;
    }
    .companies > * {
        margin: 0.5rem 0.25rem;
    }
</style>
