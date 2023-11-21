<template>
  <div class="card">
    <div class="card-body">
      <router-link class="card-title h5" v-if="link" :to="`/audio/${audio.slug}`">{{ audio.name }}</router-link>
      <h5 class="card-title" v-else>{{ audio.name }}</h5>
      <p class="card-text" v-for="paragraph in paragraphs">
        {{ paragraph }}
      </p>
      <div v-for="file in audio.files">
        <hr>
        <audio controls :src="file.file">
        </audio>
        <p>{{ file.notes }}</p>
      </div>
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
import { computed } from 'vue';

export interface Props {
  audio: any;
  link?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  link: () => false
});

const format = (datetime: string) => {
  return DateTime.fromISO(datetime).toFormat('dd LLL y HH:mm:ss');
};

const paragraphs = computed(() => {
  return props.audio.description.split("\r\n");
});
</script>