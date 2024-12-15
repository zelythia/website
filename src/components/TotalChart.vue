<template>
  <div class="chart">
    <Line class="asdf" :data="data" :options="options" />
  </div>
</template>

<script lang="ts">
import { Chart as ChartJS, CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend, LogarithmicScale } from "chart.js";
import { Line } from "vue-chartjs";
// import * as chartConfig from "./chartConfig.js";

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

      let response = await fetch(path);
      let data = await response.text();

      // Split the data into rows and then into columns
      let rows = data.split("\n").map((row) => row.split(","));

      // Extract header and data rows
      let headers = rows[0]; // First row as headers
      let dataRows = rows.slice(1).filter((row) => row.length === headers.length);

      dataRows.forEach((row) => {
        var value = 0;
        for (let i = 1; i < headers.length; i++) {
          value += parseInt(row[i].trim());
        }
        d.set(row[0].trim(), value);
      });

      return d;
    },

    async updateChart() {
      const CFdata = await this.fetchCSV("./data/curseforge.csv");
      const MRdata = await this.fetchCSV("./data/modrinth.csv");

      console.log(CFdata);

      const labels = Array.from(CFdata.keys());

      const datasets = [
        {
          label: "Total",
          data: Array.from(CFdata, ([key, value]) => value + MRdata.get(key)),
          borderColor: "rgb(238, 238, 238)",
          backgroundColor: "rgba(238, 238, 238, 0.6)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
        {
          label: "Curseforge",
          data: Array.from(CFdata, ([key, value]) => value),
          borderColor: "rgb(255, 120, 77)",
          backgroundColor: "rgba(255, 120, 77, 0.6)",
          cubicInterpolationMode: "monotone",
          tension: 0.4,
        },
        {
          label: "Modrinth",
          data: Array.from(MRdata, ([key, value]) => value),
          borderColor: "rgb(27, 217, 106)",
          backgroundColor: "rgba(27, 217, 106, 0.26)",
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
