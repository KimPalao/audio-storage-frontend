<script setup lang="ts">
import axios from 'axios';
import { onMounted, ref, watch } from 'vue';

const audio = ref([]);

const explicit = ref(false);

const getAudio = async () => {
  let url = `${import.meta.env.VITE_API_URL}/audio/`;
  if (explicit.value) {
    url += "?explicit";
  }
  const response = await axios.get(url);
  audio.value = response.data.results;
};

onMounted(getAudio);
watch(explicit, getAudio);
</script>

<template>
  <main>
    <div class="container mt-4">
      <div class="row justify-content-end mt-4">
        <div class="col-auto">
          <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" role="switch" id="showExplicit" v-model="explicit">
            <label class="form-check-label" for="showExplicit">Show NSFW</label>
          </div>

        </div>
      </div>
      <div class="card my-4" v-for="file in audio" :key="file.id">
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
<style>
.form-check-input:checked {
  background-color: #fd0ddf57;
  border-color: #fd0ddf57;
}
</style>