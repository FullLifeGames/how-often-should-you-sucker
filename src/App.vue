<template>
  <div id="app">
    <NavbarHeader />
    <b-container class="text-center sucker-container">
      <div class="p-5 mb-4 rounded-3">
        <h1 class="mb-3">How Often Should You Sucker?</h1>
        <p class="fst-italic">
          How often should you use the move Sucker Punch in a 1v1 mindgame?
          Credits to
          <a
            href="https://www.smogon.com/forums/threads/there-is-no-way-to-outplay-sucker-punch.3733939/"
            target="_blank"
            >bbg</a
          >!
        </p>
        <b-form-group label="PP" label-cols="4" label-cols-lg="2" class="mb-3">
          <b-form-input v-model="pp" type="number" />
        </b-form-group>
        <b-form-group class="mb-3">
          <b-button @click="randomize">Show me</b-button>
        </b-form-group>
        <div v-if="showOdds">
          <h2>You should sucker:</h2>
          <p>{{ whenSucker }} Times</p>
          <p class="fst-italic">
            You have a winning chance of {{ pp }}/{{ Number(pp) + 1 }}!
          </p>
        </div>
      </div>
    </b-container>
  </div>
</template>

<script setup lang="ts">
const pp = ref(8);

function randomIntFromInterval(min: number, max: number) {
  // min and max included
  return Math.floor(Math.random() * (max - min + 1) + min);
}

const whenSucker = computed(() => {
  return randomIntFromInterval(1, Number(pp.value) + 1) - 1;
});

const showOdds = ref(false);

const randomize = () => {
  showOdds.value = true;
};
</script>

<style scoped>
.sucker-container {
  margin-top: 0.5rem;
}
</style>

<style>
[data-bs-theme="dark"] .b-form-tags.focus {
  color: var(--bs-primary-text-emphasis);
  background-color: var(--bs-primary-bg-subtle);
}
[data-bs-theme="dark"] .v-select ul {
  background-color: var(--bs-primary-bg-subtle);
}
</style>
