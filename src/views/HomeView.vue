<script setup lang="ts">
import axios from 'axios';
import { onMounted, ref } from 'vue';

const audio = ref([]);

const getAudio = async () => {
  const response = await axios.get(`${import.meta.env.VITE_API_URL}/audio/`);
  audio.value = response.data.results;
};

onMounted(getAudio);
</script>

<template>
  <main>
    <div v-for="file in audio" :key="file.id">
      <h3>{{ file.name }}</h3>
      <p>{{ file.description }}</p>
    </div>
  </main>
</template>
