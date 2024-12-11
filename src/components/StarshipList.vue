<template>
    <div>
      <ul>
        <li v-for="ship in starships" :key="ship.name">
          <p>{{ ship.name }}</p>
          <button
            @click="showPilots(ship.pilots)"
            :disabled="!ship.pilots.length"
          >
            Дивитись пілотів
          </button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'StarshipList',
    props: ['onPageChange'],
    data() {
      return {
        starships: [],
        previous: null,
        next: null,
      };
    },
    async created() {
      const response = await fetch('https://swapi.dev/api/starships/');
      const data = await response.json();
      this.starships = data.results;
      this.previous = data.previous;
      this.next = data.next;
  
      // Передаем пагинацию в родительский компонент
      this.$emit('onPageChange', data);
    },
    methods: {
      showPilots(pilotUrls) {
        this.$emit('showPilots', pilotUrls);
      },
    },
  };
  </script>
  