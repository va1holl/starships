<template>
  <div>
    <button @click="prevPage" :disabled="!previous">Назад</button>
    <button @click="nextPage" :disabled="!next">Вперед</button>
  </div>
</template>

<script>
export default {
  name: 'StarshipPagination',
  props: ['previous', 'next', 'onPageChange'],
  methods: {
    prevPage() {
      if (this.previous) this.onPageChange(this.previous);
    },
    nextPage() {
      if (this.next) this.onPageChange(this.next);
    },
  },
};
</script>
