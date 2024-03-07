<template>
  <PageLayout>
    <section class="p-16">
      <PersonCard :person="person" />
    </section>
  </PageLayout>
</template>

<script>
import { mapGetters } from 'vuex'
import PageLayout from '../parts/PageLayout.vue';
import PersonCard from '@/components/cards/PersonCard.vue';

export default {
  name: 'PersonPage',
  components: {
    PageLayout,
    PersonCard
  },
  computed: {
    ...mapGetters('persons', [
      'getPersonById'
    ]),
    person () {
      return this.getPersonById(this.id)
    },
    id () {
      return this.$route.params.id
    }
  }
};
</script>
