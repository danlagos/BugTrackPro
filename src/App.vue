<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="layout">
      <nav>
        <RouterLink to="/">Home</RouterLink> |
        <router-link to="/dashboard">Dashboard</router-link>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
