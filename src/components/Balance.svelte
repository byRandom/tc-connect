<script lang="ts">
    export let balance: any;
    export let raven: Boolean;
</script>

<div class="col-sm-4 m-2 mt-3">
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">Balance</h5>
            {#if raven}
                <p class="card-text">
                    Pendiente: {Math.round(balance.pending)} RVN
                </p>
                <p class="card-text">
                    Resuelto: {Math.round(balance.cleared)} RVN
                </p>
            {:else}
                <p class="card-text">
                    Pendiente: {Math.round(balance.pending)} ETH
                </p>
                <p class="card-text">
                    Resuelto: {Math.round(balance.cleared)} ETH
                </p>
            {/if}
        </div>
    </div>
</div>

<style>
</style>
