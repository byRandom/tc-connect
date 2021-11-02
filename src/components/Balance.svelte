<script lang="ts">
    export let balance: any;
</script>

<div class="col-sm-4 m-2 mt-3">
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">Balance</h5>
            <p class="card-text">
                Pendiente: {Math.round(balance.pending)} RVN
            </p>
            <p class="card-text">Resuelto: {Math.round(balance.cleared)} RVN</p>
        </div>
    </div>
</div>

<style>
</style>
