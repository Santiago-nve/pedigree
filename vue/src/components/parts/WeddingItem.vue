<template>
  <div class="wedding-card">
    <div class="wedding-card__partner">{{ fullName }}</div>
    <div class="wedding-card__date">
      {{ wedding.startDate }}<template v-if="wedding.endDate"> - {{ wedding.endDate }}</template>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { formatPersonName } from '@/services/formatPersonName';

export default {
  name: 'WeddingItem',
  props: {
    wedding: {
      type: Object,
      required: true
    }
  },
  computed: {
    ...mapGetters ('persons', [
      'getPersonById'
    ]),
    getPartner () {
      return this.getPersonById(this.wedding.partnerId)
    },
    fullName () {
      if (this.getPartner) {
        return formatPersonName(this.getPartner, {short: true, access: this.needHide})
      }
      return ''
    }
  }
}
</script>

<style scoped lang ="less">
.wedding-card {
  background-color: #f5f5f5;
  box-shadow: 1.5px 7px 5px 1.5px rgba(0, 0, 0, 0.1), -1.5px 7px 5px -1.5px rgba(0, 0, 0, 0.2);
  border-radius: 24px;
  display: grid;
  grid-gap: 15px;
  margin-bottom: 15px;
  padding: 20px;
  padding-left: 25px;
  margin-bottom: 10px;
  text-align: center;
  max-width: 400px;

  &__partner {
    font-family: 'Inter', sans-serif;
    color: #000000;
    grid-column: span 2;
    white-space: nowrap;
    font-weight: 700;
  }

  &__date {
    font-family: 'Inter', sans-serif;
    color: #757575;
    font-weight: 700;
    white-space: nowrap;
  }
}
</style>
