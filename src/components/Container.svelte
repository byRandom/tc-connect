<script lang="ts">
    import Balance from "./Balance.svelte";
    import Earnings from "./Earnings.svelte";
    import Chart from "./Chart.svelte";
    export let walletList: any[];
    export let raven: Boolean;
</script>

<div class="accordion">
    {#each walletList as id}
        <div class="accordion-item">
            <h2 class="accordion-header" id="heading-{id.wallet}">
                <button
                    class="accordion-button"
                    type="button"
                    data-bs-toggle="collapse"
                    data-bs-target="#collapse-{id.wallet}"
                    aria-expanded="true"
                    aria-controls="collapseOne"
                >
                    {id.apiType}:
                    {id.wallet}
                </button>
            </h2>
            <div
                id="collapse-{id.wallet}"
                class="accordion-collapse collapse show"
                aria-labelledby="heading-{id.wallet}"
                data-bs-parent="#{id.wallet}"
            >
                <div class="accordion-body">
                    <div class="row">
                        <div class="col">
                            <h4>Ganancias</h4>
                            <Balance balance={id.balance} {raven} />
                            <Earnings
                                raven={id.raven}
                                d1={id.data.d1}
                                d7={id.data.d7}
                                d14={id.data.d14}
                                d30={id.data.d30}
                                d90={id.data.d90}
                            />
                        </div>
                        <div class="col-sm-4">
                            <Chart
                                walletID={id.wallet}
                                historyData={id.historyData}
                            />
                        </div>
                        <div class="col-sm-4">
                            <h4>Payouts</h4>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    {/each}
</div>
