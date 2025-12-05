<template>
  <div class="home-page">
    <SubnetCalculator />
  </div>
</template>

<script setup lang="ts">
import SubnetCalculator from '@/components/SubnetCalculator.vue';
</script>

<style scoped>
.home-page {
  padding: 20px;
  background-color: #f5f5f5;
  min-height: 100vh;
}
</style>
