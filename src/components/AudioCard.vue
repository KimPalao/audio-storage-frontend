<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ audio.name }}</h5>
      <p class="card-text">{{ audio.description }}</p>
      <audio controls :src="audio.file">
      </audio>
    </div>
    <div class="card-footer text-end">
      {{ audio.created_at }}
    </div>
  </div>
</template>
<script setup lang="ts">
defineProps<{
  audio: any;
}>();
</script>