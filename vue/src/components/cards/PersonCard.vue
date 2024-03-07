<template>
  <div class="person-card">
    <div>
      <PhotoPreview size="large" />
    </div>
    <div>
      <h1>{{ fullName }}</h1>
      <span class="person-card__dates">{{ person.birth_date }}</span>
      <span v-if="person.die_date" class="person-card__dates"> - {{ person.die_date }}</span>

      <h2>Родители</h2>
      <div class="person-card__information-text">
        <RelateButton :person="person" relate="parent" />
      </div>

      <h2>Дети </h2>
      <div class="person-card__information-text">
        <RelateButton :person="person" relate="child" />
      </div>

      <h2>Род деятельности</h2>
      <div class="person-card__information-text">
        {{ person.activity || 'Информации нет' }}
      </div>

      <h2>Биография</h2>
      <div class="person-card__information-text">
        {{ person.biography || 'Информации нет' }}
      </div>

      <h2>Брачные союзы</h2>
      <WeddingsList
        v-if="person.weddings.length > 0"
        :weddings="person.weddings"
      />
      <div v-else class="person-card__information-text">
        Информации нет
      </div>
    </div>
  </div>
</template>

<script>
import WeddingsList from '../parts/WeddingsList.vue';
import PhotoPreview from '../ui/PhotoPreview.vue';
import RelateButton from '@/components/ui/RelateButton.vue';

export default {
  name: 'PersonCard',
  components: {
    WeddingsList,
    PhotoPreview,
    RelateButton
  },
  props: {
    person: {
      type: Object,
      required: true
    }
  },
  computed: {
    fullName () {
      return `${this.person.secondName} ${this.person.firstName} ${this.person.patronymicName}`;
    }
  }
}
</script>

<style scoped lang ="less">
.person-card {
  display: flex;
  gap: 15px;

  &__dates {
    font-size: 12px;
    color: grey;
    padding-bottom: 20px;
  }

  &__information-text {
    font-weight: 500;
    font-size: 10px;
    padding-bottom: 20px;
    color: black;
  }
}
</style>
