<script setup lang="ts">
import { ref, onMounted } from "vue";
import BalanceCard from "./components/BalanceCard.vue";
import WeeklySpendChartCard from "./components/WeeklySpendChartCard.vue";
let datas = ref([Object]);

async function fetchData() {
  const response = await fetch("/data.json");
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  } else {
    datas.value = await response.json();
    return datas.value;
  }
}
onMounted(() => {
  console.log(datas.value);

  fetchData();
});
</script>
<template>
  <div class="container">
    <BalanceCard />
    <div class="spending_card">
      <h1>Spending - Last 7 days</h1>
      <!-- <WeeklySpendChartCard :datas="datas" /> -->
      <div class="spend_monthly">
        <div class="this_month">
          <p>Total this month</p>
          <h2>$478.33</h2>
        </div>
        <div class="last_month">
          <p>+2.4%</p>
          <p>from last month</p>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  gap: 2rem;
  align-items: center;
  height: 100vh;
}
.spending_card {
  background: var(--vt-c-white-soft);
  border-radius: 0.6rem;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  align-items: center;
  height: 30rem;
  padding: 1rem 2rem;
  width: 75%;
}

.spend_monthly {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}
h2 {
  font-size: 1.5rem;
  font-weight: 700;
}
p {
  font-size: 1rem;
  color: var(--vt-c-text-light-2);
}
.this_month,
.last_month {
  display: flex;
  flex-direction: column;
}
.this_month {
  align-items: flex-start;
}
.last_month {
  align-items: flex-end;
}
.last_month p:first-of-type {
  font-weight: 700;
  color: #000;
}
</style>
