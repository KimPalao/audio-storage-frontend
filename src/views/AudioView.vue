<script setup lang="ts">
import axios from 'axios';
import { onMounted, ref, watch, type Ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import * as bootstrap from 'bootstrap';
import AudioCard from '@/components/AudioCard.vue';

const route = useRoute();
const router = useRouter();

const audio: any = ref({});

const explicit = ref(false);

const hasConfirmed = ref(localStorage.getItem("hasConfirmed"));

const getAudio = async () => {
  let url = `${import.meta.env.VITE_API_URL}/audio/${route.params.slug}/`;
  const response = await axios.get(url);
  audio.value = response.data;
  if (audio.value.explicit && !hasConfirmed.value) {
    confirmationModal.show();
  }
};

const confirmationModalElement: Ref<Element> = ref(document.createElement('div'));

let confirmationModal: any = null;

const confirm = () => {
  confirmationModal.hide();
  localStorage.setItem('hasConfirmed', "true");
  hasConfirmed.value = "true";
};

const back = () => {
  confirmationModal.hide();
  router.push("/");
};

onMounted(() => {
  getAudio();
  confirmationModal = new bootstrap.Modal(confirmationModalElement.value);
});
watch(explicit, getAudio);
</script>

<template>
  <main>
    <div class="container mt-4" v-if="!audio.explicit || (audio.explicit && hasConfirmed)">
      <audio-card :audio="audio"></audio-card>
    </div>

    <div class="modal" tabindex="-1" ref="confirmationModalElement">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Confirm</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <p>Toggling this setting will display adult content. By clicking continue, you confirm that you are of legal
              age to view adult material.</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="back">Close</button>
            <button type="button" class="btn btn-primary" @click="confirm">Continue</button>
          </div>
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