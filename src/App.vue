<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router';
import HelloWorld from './components/HelloWorld.vue';
</script>

<template>
  <RouterView />
  <footer>
    Kim Palao
  </footer>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

footer {
  border-top: 1px solid #666;
  padding: 2em;
  text-align: center;
}
</style>
