<script setup lang="js">
import Chart from "chart.js/auto";
import { ref, onMounted, onBeforeUnmount, watch } from "vue";

const props = defineProps(["weeklydatas"]);
let dataSet = ref([])
let dayName = ref([])
let setBarThickness = ref(30)

props.weeklydatas.map((data) => dataSet.value.push(data.amount))
props.weeklydatas.map((data) => dayName.value.push(data.day))
const windowsWidth = ref(window.innerWidth);

const updateWindowsWidth = () => {
  windowsWidth.value = window.innerWidth;
};
watch(() => windowsWidth.value, () => {
  if (windowsWidth.value >= 1024) {
    setBarThickness.value = 40;
  } else if (windowsWidth.value >= 768 && windowsWidth.value < 1024) {
    setBarThickness.value = 40;
  } else {
    setBarThickness.value = 10;
  }
  console.log( setBarThickness.value);
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateWindowsWidth);
});

onMounted(() => {

  const ctx = document.getElementById("dimensions");
  window.addEventListener('resize', updateWindowsWidth);

  new Chart(ctx, {
    type: "bar",
    maintainAspectRatio: true,
    data: {
      labels: dayName.value,
      datasets: [
        {
          data: dataSet.value,
          label: '',
          backgroundColor: [
          "hsl(10, 79%, 65%)"
          ],
          hoverBackgroundColor: [
            "hsl(186, 34%, 60%)"
          ],
          borderColor: "transparent",
          barThickness: setBarThickness.value,
          borderRadius: 7,
        },
      ],
    },
    options: {
      responsive: true,
      plugins: {
        legend: {
          display: false,
        },
        tooltip: {
           displayColors: false,
                callbacks: {
                  title: function() {
                    return '';
                  },
                    label: function(context) {
                        let label = context.dataset.label;
                        if (context.parsed.y !== null) {
                            label += new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(context.parsed.y);
                        }
                        return label;
                    }
                },
            }
      },
      scales: {
        y: {
          display: false,
          beginAtZero: true,
          grid: {
            display: false,
          }
        },
        x: {
          display: true,
          grid: {
            display: false,
          }
        },
      },
    },
  });
})
</script>
<template>
  <div class="chart">
    <canvas id="dimensions"></canvas>
  </div>
</template>

<style scoped>
.chart {
  width: 100%;
  border-bottom: 2.5px solid var(--vt-c-cream);
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 3rem;
  height: 25rem;
}

@media screen and (min-width: 1024px) {
  .chart {
    margin-bottom: 1.5rem;
  }
}


</style>
