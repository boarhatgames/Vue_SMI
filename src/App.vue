<template>
  <v-app theme="dark">
    <Header />
    <v-main>
      <router-view :items="items" />
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    Header,
  },
  data() {
    return {
      items: [],
    };
  },
  methods: {
    // eslint-disable-next-line no-console
    log(...args) {
      console.log(...args);
    },

    async getItems() {
      const response = await fetch('/api/items');
      const data = await response.json();
      return data;
    },
  },
  async created() {
    this.items = await this.getItems();
  },
};
</script>
