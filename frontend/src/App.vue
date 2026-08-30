<template>
  <div>
    <h1>MasterOfTickets</h1>
    <p>Welcome to the ticket comparison platform</p>
    <router-view />
  </div>
</template>

<script setup>
import { RouterView } from 'vue-router';
</script>
<style scoped>
h1 {
  color: #3b82f6;
}
</style>