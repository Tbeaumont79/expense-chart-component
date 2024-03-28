<script setup>
import { ref, onMounted, reactive } from "vue";
import BalanceCard from "./components/BalanceCard.vue";
import WeeklySpendChartCard from "./components/WeeklySpendChartCard.vue";

const states = reactive({
  datas: null, // Initialisez à null plutôt qu'à [{}]
});

async function fetchDatas() {
  try {
    const response = await fetch("/data.json");
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const result = await response.json();
    return result;
  } catch (error) {
    console.error("Erreur lors de la récupération des données :", error);
    return null; // Retournez null en cas d'erreur
  }
}
onMounted(async () => {
  states.datas = await fetchDatas();
});
</script>
<template>
  <div class="container">
    <BalanceCard />
    <div class="spending_card">
      <h1>Spending - Last 7 days</h1>
      <WeeklySpendChartCard v-if="states.datas" :weeklydatas="states.datas" />
      <div class="spend_monthly">
        <div class="this_month">
          <p>Total this month</p>
          <h2 class="amount">$478.33</h2>
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
  height: 25rem;
  padding: 1rem 2rem;
  width: 75%;
}

.spending_card h1:first-of-type {
  align-self: start;
}

.spend_monthly {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}
h1 {
  font-size: 1.5rem;
  font-weight: bold;
}
.amount {
  font-size: 2rem !important;
  font-weight: bold;
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

@media screen and (min-width: 768px) {
  .spending_card {
    width: 30rem;
    height: 30rem;
  }
}

@media screen and (min-width: 1440px) {
  .container {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    gap: 2rem;
    align-items: center;
  }
  .spending_card {
    width: 30rem;
    height: 30rem;
  }
  h1 {
    font-size: 2rem;
  }
  .amount {
    font-size: 3rem !important;
    font-weight: bold;
  }
  p {
    font-size: 1.5rem;
  }
}
</style>
