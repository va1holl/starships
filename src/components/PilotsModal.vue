<template>
    <div v-if="isVisible" class="modal">
      <div class="modal-content">
        <h3>Пилоты</h3>
        <ul>
          <li v-for="pilot in pilots" :key="pilot.name">
            {{ pilot.name }}
          </li>
        </ul>
        <button @click="closeModal">Закрыть</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PilotsModal',
    props: ['pilotUrls'],
    data() {
      return {
        pilots: [],
        isVisible: false,
      };
    },
    watch: {
      pilotUrls: {
        immediate: true,
        handler(newUrls) {
          this.fetchPilots(newUrls);
        },
      },
    },
    methods: {
      async fetchPilots(urls) {
        this.pilots = [];
        for (const url of urls) {
          const response = await fetch(url);
          const data = await response.json();
          this.pilots.push(data);
        }
      },
      closeModal() {
        this.isVisible = false;
      },
      openModal() {
        this.isVisible = true;
      },
    },
  };
  </script>
  
  <style>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  </style>
  