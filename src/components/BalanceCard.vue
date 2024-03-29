<script setup lang="ts"></script>
<template>
  <div class="balance_card">
    <div class="current_balance">
      <h2>My balance</h2>
      <p>$921.48</p>
    </div>
    <img src="/Images/logo.svg" alt="" />
  </div>
</template>

<style scoped>
.balance_card {
  background: var(--vt-c-red-soft);
  border-radius: 0.6rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 5rem;
  padding: 1rem 2rem;
  width: 75%;
}
.current_balance {
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  flex-direction: column;
}
h2,
p {
  color: var(--vt-c-white);
}
h2 {
  font-size: 1rem;
  font-weight: 400;
  opacity: 0.8;
}
p {
  font-size: 1.5rem;
  font-weight: 700;
}
img {
  height: 4rem;
  width: 4rem;
}

@media screen and (min-width: 768px) {
  .balance_card {
    width: 20rem;
  }
}
@media screen and (min-width: 1440px) {
  .balance_card {
    width: 30rem;
  }
  h2 {
    font-size: 1.5rem;
  }
  p {
    font-size: 2rem;
  }
}
</style>
