<template>
  <div class="chart">
    <Line class="asdf" :data="data" :options="options" />
  </div>
</template>

<script lang="ts">
import { Chart as ChartJS, CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend, LogarithmicScale, Ticks } from "chart.js";
import { Line } from "vue-chartjs";

// eslint-disable-next-line prettier/prettier
  ChartJS.register(
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
    LogarithmicScale
  )

ChartJS.defaults.color = "#ccc";
ChartJS.defaults.borderColor = "rgba(204, 204, 204, 0.2)"; //#ccc

const tickValues = [50, 100, 200, 500, 1000, 10000, 50000, 100000, 200000];

export default {
  name: "App",
  components: {
    // eslint-disable-next-line vue/no-reserved-component-names
    Line,
  },
  data() {
    return {
      // Default chart data and options
      data: {
        labels: [],
        datasets: [],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            position: "bottom",
          },
        },
        scales: {
          x: {
            display: true,
            grid: {
              display: false,
            },
          },
          y: {
            display: true,
            type: "logarithmic",
            min: 1,
            max: tickValues[tickValues.length-1],
            ticks: {
              values: tickValues,
            },
            grid: {
              drawTicks: true,
              drawBorder: true,
            },
            afterBuildTicks: function (axis) {
              // Force consistent ticks
              axis.ticks = tickValues.map((value) => ({ value }));
            },
          },
        },
        interaction: {
          mode: "index",
          intersect: false,
          callbacks: {
            label: function (tooltipItem) {
              return `${tooltipItem.dataset.label}: ${tooltipItem.raw}`;
            },
          },
          itemSort: function (a, b) {
            return b.raw - a.raw; // Sort descending by value
          },
        },
        elements: {
          point: {
            pointStyle: false,
          },
        },
      },
    };
  },
  methods: {
    async fetchCSV(path) {
      let d = new Map();

      //---------CURSEFORGE-------------
      let response = await fetch(path);
      let data = await response.text();

      // Split the data into rows and then into columns
      let rows = data.split("\n").map((row) => row.split(","));

      // Extract header and data rows
      let headers = rows[0]; // First row as headers
      let dataRows = rows.slice(1).filter((row) => row.length === headers.length);

      dataRows.forEach((row) => {
        var values = [];
        for (let i = 1; i < headers.length; i++) {
          values.push(parseInt(row[i].trim()));
        }
        d.set(row[0].trim(), values);
      });

      return d;
    },

    async updateChart() {
      const CFdata = await this.fetchCSV("./data/curseforge.csv");
      const MRdata = await this.fetchCSV("./data/modrinth.csv");

      const labels = Array.from(CFdata.keys());

      const datasets = [
        {
          label: "AutoTools",
          data: Array.from(CFdata, ([key, values]) => values[0] + MRdata.get(key)[0]),
          borderColor: "rgb(122, 199, 64)",
          backgroundColor: "rgba(122, 199, 64, 0.6)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
        {
          label: "Aequitas",
          data: Array.from(CFdata, ([key, values]) => values[1] + MRdata.get(key)[1]),
          borderColor: "rgb(1, 226, 186)",
          backgroundColor: "rgba(1, 226, 186, 0.26)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
        {
          label: "Equal Sky!",
          data: Array.from(CFdata, ([key, values]) => values[2] + MRdata.get(key)[2]),
          borderColor: "rgb(64, 197, 199)",
          backgroundColor: "rgba(64, 197, 199, 0.6)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
        {
          label: "Equal Sky! - Companion",
          data: Array.from(CFdata, ([key, values]) => values[3] + MRdata.get(key)[3]),
          borderColor: "rgb(165, 201, 201)",
          backgroundColor: "rgba(165, 201, 201, 0.6)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
        {
          label: "Fabricae Ex Nihilo - AE2 Addon",
          data: Array.from(CFdata, ([key, values]) => values[4] + MRdata.get(key)[4]),
          borderColor: "rgba(255, 159, 64, 1)",
          backgroundColor: "rgba(255, 159, 64, 0.6)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
      ];

      this.data = {
        labels,
        datasets,
      };
    },
  },

  async mounted() {
    await this.updateChart();
  },
};
</script>

<style></style>
