<script lang="ts">
    import Navbar from "./components/Navbar.svelte";
    import axios from "axios";
    import Balance from "./components/Balance.svelte";
    import Loading from "./components/Loading.svelte";
    import Container from "./components/Container.svelte";

    let check: Boolean = false;
    let api: string;
    let raven: Boolean = true;
    // let wallet: string = raven
    //     ? "RF7qc6sHVnCgNYFk11usQGLV1U9H5eTDLw"
    //     : "98a4073f6ba849065c71e03bb0a81d863fbdc72c";
    let wallet: string = "";
    let balance: string = "";
    let earnings: any;
    let walletList: any[] = [];
    let walletAmmount: number = 0;
    let miningData = {
        d1: 0,
        d7: 0,
        d14: 0,
        d30: 0,
        d90: 0,
    };
    let hashrate: any[];
    //Navbar

    const ravenSwitch = () => {
        raven = !raven;
        console.log(raven);
    };

    const addWallet = (wallet: string, apiType, data, balance) => {
        check = false;
        walletList.forEach((value, index) => {
            if (walletList[index].wallet === wallet) {
                console.log("wallet in walletList");
                check = true;
            }
        });
        if (!check) {
            walletList.push({
                wallet: wallet,
                apiType: apiType,
                raven: raven,
                data: data,
                balance: balance,
            });
            console.log(walletList[-1]);
        }
    };
    const getWallet = async (walletAddr: string) => {
        if (walletAddr.trim()) {
            api = raven
                ? `https://www.ravenminer.com/api/v1/wallet/${walletAddr}`
                : `https://api.ethermine.org/miner/:${walletAddr}/dashboard`;
            let { data, status } = await axios.get(api);
            if ((status = 200)) {
                if (raven) {
                    balance = data.balance;
                    earnings = data.earnings;
                    console.log(data, status);
                    miningData.d1 = earnings["1d"];
                    miningData.d7 = earnings["7d"];
                    miningData.d14 = earnings["14d"];
                    miningData.d30 = earnings["30d"];
                    miningData.d90 = earnings["90d"];
                    addWallet(walletAddr, "Raven", miningData, balance);
                    console.log(miningData);
                    console.log(walletList);
                } else {
                    if (data.status === "ERROR") {
                        throw new Error(data.error);
                    }
                    addWallet(walletAddr, "Ethereum", miningData, balance);
                    console.log(walletList);
                }
            } else {
                throw new Error("Unreachable");
            }
        } else {
            console.log("search empty");
        }
    };

    let promise = getWallet(wallet);

    let handleSubmit = (walletSearch: string = wallet) => {
        promise = getWallet(walletSearch);
    };
</script>

<Navbar {raven} {handleSubmit} {wallet} {ravenSwitch} />
{#await promise}
    <div class="row bg-secondary">
        <Loading />
    </div>
{:then}
    <div class="row bg-secondary">
        <Container {walletList} />
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
