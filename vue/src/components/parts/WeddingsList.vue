<template>
  <div v-if="weddings" class="weddings-list">
    <WeddingItem v-for="(wedding, index) in weddings" :key="index" :wedding="wedding" />
  </div>
</template>

<script>
import WeddingItem from './WeddingItem.vue';

export default {
  name: 'WeddingsList',
  components: {
    WeddingItem
  },
  props: {
    weddings: {
      type: Array,
      required: true
    }
  }
};
</script>
