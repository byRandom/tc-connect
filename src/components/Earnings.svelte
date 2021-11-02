<script lang="ts">
    export let d1: number;
    export let d7: number;
    export let d14: number;
    export let d30: number;
    export let d90: number;
    export let raven: Boolean;
</script>

<div class="col-sm-4 m-2 mt-3">
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">Ganancias</h5>
            {#if raven}
                <p class="card-text text-center">1D: {Math.round(d1)} RVN</p>
                <p class="card-text text-center">7D: {Math.round(d7)} RVN</p>
                <p class="card-text text-center">14D: {Math.round(d14)} RVN</p>
                <p class="card-text text-center">30D: {Math.round(d30)} RVN</p>
                <p class="card-text text-center">90D: {Math.round(d90)} RVN</p>
            {:else}
                <p class="card-text text-center">ETHEREUM DETECTED BRUH</p>
            {/if}
        </div>
    </div>
</div>

<style>
    p {
        border-radius: 20px;
        background-color: #0d6efd;
        color: #fff;
    }
</style>
