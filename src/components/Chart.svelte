<script lang="ts">
    import Line from "svelte-chartjs/src/Line.svelte";
    export let historyData: any[];
    export let walletID;
    let dataList: any[] = [];
    historyData.forEach((_, index) => {
        let amount: Number = historyData[index].amount;
        let time: number = historyData[index].time;
        dataList.push({ amount: amount, time: time });
    });

    console.log(dataList, "DEBUG");
    let labels = [];
    let amount = [];
    dataList.forEach((_, index) => {
        let unix_timestamp = dataList[index].time;
        // Create a new JavaScript Date object based on the timestamp
        // multiplied by 1000 so that the argument is in milliseconds, not seconds.
        let date = new Date(unix_timestamp * 1000);
        // Hours part from the timestamp
        let hours = date.getHours();
        // Minutes part from the timestamp
        let minutes = date.getMinutes();
        // Seconds part from the timestamp
        let seconds = date.getSeconds();
        //Get Day
        let day = date.getDate();
        //Get month
        let month = date.getMonth();
        //Get Year
        let year = date.getFullYear();
        // Will display time in 10:30:23 format
        let labelDate = `${day}-${month}-${year} ${hours}:${minutes}`;
        labels.push(labelDate);
        console.log(labels);

        amount.push(dataList[index].amount);
        console.log(amount);
    });

    let dataLine = {
        labels: labels,
        datasets: [
            {
                label: "PPLNS Reward",
                fill: true,
                lineTension: 0.3,
                backgroundColor: "rgba(225, 204,230, .3)",
                borderColor: "rgb(205, 130, 158)",
                borderCapStyle: "butt",
                borderDash: [],
                borderDashOffset: 0.0,
                borderJoinStyle: "miter",
                pointBorderColor: "#f85bc4",
                pointBackgroundColor: "rgb(255, 255, 255)",
                pointBorderWidth: 4,
                pointHoverRadius: 5,
                pointHoverBackgroundColor: "rgb(0, 0, 0)",
                pointHoverBorderColor: "#f85bc4",
                pointHoverBorderWidth: 2,
                pointRadius: 1,
                pointHitRadius: 10,
                data: amount,
            },
        ],
    };
</script>

<div id={walletID}>
    <h4>Recompensas PPLNS</h4>
    <div class="chart">
        <Line data={dataLine} />
    </div>
</div>

<style>
    .chart {
        max-width: 100%;
    }
</style>
