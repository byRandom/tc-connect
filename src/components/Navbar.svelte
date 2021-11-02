<script lang="ts">
    export let raven: Boolean;
    export let handleSubmit: any;
    export let wallet: string;
    export let ravenSwitch;
</script>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
        <a href="/" class="navbar-brand"
            ><img src="/images/Tc-Logo.jpg" alt="ToastCorp logo" />TC Connect</a
        >
        <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
        >
            <span class="navbar-toggler-icon" />
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0" />
            <div class="form-check form-switch">
                <input
                    class="form-check-input"
                    type="checkbox"
                    role="switch"
                    id="flexSwitchCheckDefault"
                    on:click={ravenSwitch}
                />
                <label
                    class="form-check-label bg-dark"
                    for="flexSwitchCheckDefaut">Raven/Ethereum</label
                >
            </div>
            <form
                on:submit|preventDefault={() => handleSubmit(wallet)}
                class="d-flex"
            >
                <input
                    bind:value={wallet}
                    class="form-control me-2"
                    type="search"
                    placeholder="Wallet"
                    aria-label="Search"
                />
                <button class="btn btn-outline-success" type="submit"
                    >Buscar</button
                >
            </form>
        </div>
    </div>
</nav>

<style>
    img {
        max-width: 30px;
        border-radius: 15px;
        margin-right: 10px;
    }
    label {
        color: white;
        margin-right: 10px;
    }
</style>
