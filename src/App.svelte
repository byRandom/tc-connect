<script lang="ts">
    import Navbar from "./components/Navbar.svelte";
    import axios from "axios";
    import Balance from "./components/Balance.svelte";
    import Earnings from "./components/Earnings.svelte";
    import Loading from "./components/Loading.svelte";

    let api: string;
    let raven: Boolean = true;
    let wallet: string = raven
        ? "RF7qc6sHVnCgNYFk11usQGLV1U9H5eTDLw"
        : "98a4073f6ba849065c71e03bb0a81d863fbdc72c";
    let balance: string = "";
    let earnings;
    let d1: number;
    let d7: number;
    let d14: number;
    let d30: number;
    let d90: number;
    let hashrate: any[];
    //Navbar
    const ravenSwitch = () => {
        raven = !raven;
        console.log(raven);
    };

    const getWallet = async (walletAddr: string = wallet) => {
        api = raven
            ? `https://www.ravenminer.com/api/v1/wallet/${walletAddr}`
            : `https://api.ethermine.org/miner/:${walletAddr}/dashboard`;

        console.log(api);
        let { data, status } = await axios.get(api);
        if ((status = 200)) {
            if (raven) {
                balance = data.balance;
                earnings = data.earnings;
                console.log(data, status);
                d1 = earnings["1d"];
                d7 = earnings["7d"];
                d14 = earnings["14d"];
                d30 = earnings["30d"];
                d90 = earnings["90d"];
            } else {
                if (data.status === "ERROR") {
                    throw new Error(data.error);
                }
            }
        } else {
            throw new Error("Unreachable");
        }
    };

    let promise = getWallet(wallet);

    let handleSubmit = (walletSearch: string = wallet) => {
        promise = getWallet(walletSearch);
    };
    //

    //Balance
    //
</script>

<Navbar {raven} {handleSubmit} {wallet} {ravenSwitch} />
{#await promise}
    <Loading />
{:then}
    <div class="row bg-secondary">
        <Balance {balance} />
    </div>
    <div class="row bg-secondary">
        <Earnings {raven} {d1} {d7} {d14} {d30} {d90} />
    </div>
{:catch err}
    <div class="alert alert-danger" role="alert">
        {err}
    </div>
{/await}

<style>
    .row {
        overflow: hidden;
        width: 100%;
        margin: 0px;
    }
</style>
