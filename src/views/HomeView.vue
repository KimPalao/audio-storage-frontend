<script setup lang="ts">
import axios from 'axios';
import { onMounted, ref, watch } from 'vue';
import * as bootstrap from 'bootstrap';

const audio: any = ref([]);

const explicit = ref(false);

const getAudio = async () => {
  let url = `${import.meta.env.VITE_API_URL}/audio/`;
  if (explicit.value) {
    url += "?explicit";
  }
  const response = await axios.get(url);
  audio.value = response.data.results;
};

const confirmationModalElement = ref(null);

let confirmationModal: any = null;

const showConfirmationModal = (event: Event) => {
  const hasConfirmed = localStorage.getItem("hasConfirmed");
  if (!hasConfirmed) {
    confirmationModal.show();
    return event.preventDefault();
  }
};

const confirm = () => {
  confirmationModal.hide();
  localStorage.setItem('hasConfirmed', "true");
  explicit.value = true;
};

onMounted(() => {
  getAudio();
  confirmationModal = new bootstrap.Modal(confirmationModalElement.value);
});
watch(explicit, getAudio);
</script>

<template>
  <main>
    <div class="container mt-4">
      <div class="row justify-content-end mt-4">
        <div class="col-auto">
          <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" role="switch" id="showExplicit" v-model="explicit"
              @click="showConfirmationModal">
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
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
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