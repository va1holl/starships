<template>
  <div id="app">
    <h1>Космические корабли</h1>
    <StarshipList @showPilots="showPilots" :onPageChange="fetchPage" />
    <StarshipPagination
      :previous="previous"
      :next="next"
      @onPageChange="fetchPage"
    />
    <PilotsModal :pilotUrls="currentPilotUrls" ref="modal" />
  </div>
</template>

<script>
import StarshipList from './components/StarshipList.vue';
import StarshipPagination from './components/StarshipPagination.vue';
import PilotsModal from './components/PilotsModal.vue';

export default {
  components: { StarshipList, StarshipPagination, PilotsModal },
  data() {
    return {
      previous: null,
      next: null,
      currentPilotUrls: [],
    };
  },
  methods: {
    async fetchPage(url) {
      const response = await fetch(url);
      const data = await response.json();
      this.previous = data.previous;
      this.next = data.next;
    },
    showPilots(pilotUrls) {
      this.currentPilotUrls = pilotUrls;
      this.$refs.modal.openModal();
    },
  },
};
</script>

<style>
/* Добавьте стили по желанию */
</style>
