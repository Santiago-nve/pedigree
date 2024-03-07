<template>
  <button
    class="relate-button"
    :class="'relate-button__' + (isMale ? 'male' : 'female')"
  >
    <template v-if="relate === 'parent'">
      {{ isMale ? 'Отец: ' : 'Мать: ' }}
    </template>
    {{ formatName }}
  </button>
</template>

<script>
export default {
  name: 'RelateButton',
  props: {
    person: {
      type: Object,
      required: true
    },
    relate: {
      type: String,
      default: 'child',
      validator: value => ['child', 'parent'].includes(value)
    }
  },
  computed: {
    isMale () {
      return this.person.gender === 'male'
    },
    formatName () {
      return `${this.person.secondName} ${this.person.firstName[0]}. ${this.person.patronymicName[0]}.`
    }
  }
};
</script>

<style scoped lang="less">
.relate-button {
  margin-right: 10px;
  margin-bottom: 10px;
  border: none;
  padding: 10px 20px;
  color: black;
  font-weight: bold;
  border-radius: 5px;
  cursor: pointer;

  &__male {
    background-color: #adffb4;
  }

  &__female {
    background-color: #adffe6;
  }
}
</style>
