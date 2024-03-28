<script setup lang="ts">
import Chart from "chart.js/auto";
import { ref, onMounted } from "vue";

const props = defineProps({
  datas: [Object],
});
const dimensions = ref();
onMounted(() => {
  const ctx = dimensions.value.getContext("2d");
  new Chart(ctx, {
    type: "bar",
    data: {
      labels: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
      datasets: [
        {
          data: props.datas.map((data) => data.amount),
          backgroundColor: "rgba(255, 99, 132, 0.5)",
        },
      ],
    },
  });
});
</script>
<template>
  <div class="chart"><canvas id="dimensions"></canvas></div>
</template>

<style scoped>
.chart {
  height: 15rem;
  width: 75%;
  background: #000;
}
</style>
