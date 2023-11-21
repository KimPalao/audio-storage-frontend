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
    <div class="container mt-4">
      <div class="card" v-for="file in audio" :key="file.id">
        <div class="card-body">
          <h5 class="card-title">{{ file.name }}</h5>
          <p class="card-text">{{ file.description }}</p>
          <audio controls :src="file.file">
          </audio>
        </div>
      </div>
    </div>
  </main>
</template>
