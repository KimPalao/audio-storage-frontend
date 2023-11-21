<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router';
import HelloWorld from './components/HelloWorld.vue';
</script>

<template>
  <header>
    <div class="container pt-4">
      <nav>
        <router-link to="/" class="brand-link">
          <h1>Audio</h1>
        </router-link>
      </nav>
    </div>
  </header>
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
