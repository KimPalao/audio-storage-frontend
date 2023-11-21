<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ audio.name }}</h5>
      <p class="card-text">{{ audio.description }}</p>
      <audio controls :src="audio.file">
      </audio>
    </div>
    <div class="card-footer text-end">
      <em>
        {{ format(audio.created_at) }}
      </em>
    </div>
  </div>
</template>
<script setup lang="ts">
import { DateTime } from 'luxon';

defineProps<{
  audio: any;
}>();

const format = datetime => {
  return DateTime.fromISO(datetime).toFormat('dd LLL y HH:mm:ss');
};
</script>