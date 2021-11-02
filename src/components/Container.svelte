<script lang="ts">
    import Balance from "./Balance.svelte";
    import Earnings from "./Earnings.svelte";
    export let walletList: any[];
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
                    <Balance balance={id.balance} />
                    <Earnings
                        raven={id.raven}
                        d1={id.data.d1}
                        d7={id.data.d7}
                        d14={id.data.d14}
                        d30={id.data.d30}
                        d90={id.data.d90}
                    />
                </div>
            </div>
        </div>
    {/each}
</div>
