<template>
  <div class="chart">
    <canvas :id="id" class="chart-canvas" :height="height"></canvas>
  </div>
</template>

<script>
import Chart from "chart.js/auto";

export default {
  props: {
    id: {
      type: String,
      default: "chart-line-1",
    },
    height: {
      type: [String, Number],
      default: "100",
    },
    chart: {
      type: Object,
      required: true,
      labels: Array,
      datasets: {
        type: Array,
        required: true,
        label: String,
        data: Array,
      },
    },
  },
  mounted() {
    var ctx1 = document.getElementById(this.id).getContext("2d");

    let chartStatus = Chart.getChart(this.id);
    if (chartStatus != undefined) {
      chartStatus.destroy();
    }

    new Chart(ctx1, {
      type: "line",
      data: {
        labels: this.chart.labels,
        datasets: [
          {
            label: this.chart.datasets.label,
            tension: 0.5,
            borderWidth: 0,
            pointRadius: 0,
            borderColor: "#fff",
            // eslint-disable-next-line no-dupe-keys
            borderWidth: 2,
            backgroundColor: "transparent",
            data: this.chart.datasets[0].data,
            maxBarThickness: 6,
            fill: true,
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            display: false,
          },
        },
        interaction: {
          intersect: false,
          mode: "index",
        },
        scales: {
          y: {
            grid: {
              drawBorder: false,
              display: false,
              drawOnChartArea: false,
              drawTicks: false,
            },
            ticks: {
              display: false,
            },
          },
          x: {
            grid: {
              drawBorder: false,
              display: false,
              drawOnChartArea: false,
              drawTicks: false,
            },
            ticks: {
              display: false,
            },
          },
        },
      },
    });
  },
};
</script>
