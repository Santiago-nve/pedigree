<template>
  <div class="custom-form">
    <ElInput
      v-model="secondName"
      class="custom-form__input"
      type="text"
      placeholder="Фамилия"
    />
    <ElInput
      v-model="firstName"
      class="custom-form__input"
      type="text"
      placeholder="Имя"
    />
    <ElInput
      v-model="patronymic"
      class="custom-form__input"
      type="text"
      placeholder="Отчество"
    />
    <ElInput
      v-model="gender"
      class="custom-form__input"
      type="text"
      placeholder="Пол"
    />
    <ElDatePicker
      v-model="birth_date"
      class="custom-form__input"
      type="date"
      format="dd.MM.yyyy"
      value-format="dd.MM.yyyy"
      placeholder="Дата рождения"
    />
    <ElDatePicker
      v-model="die_date"
      class="custom-form__input"
      type="date"
      format="dd.MM.yyyy"
      value-format="dd.MM.yyyy"
      placeholder="Дата смерти"
    />
    <div class="custom-form__full-width">
      <ElInput
        v-model="activity"
        class="custom-form__input"
        type="textarea"
        placeholder="Род деятельности"
      />
    </div>
    <div class="custom-form__full-width">
      <ElInput
        v-model="biography"
        class="custom-form__input"
        type="textarea"
        placeholder="Биография"
      />
    </div>
  </div>
</template>

<script>

export default {
  name: 'PersonForm',
  model: {
    prop: 'value',
    event: 'change'
  },
  props: {
    value: {
      type: Object,
      required: true
    }
  },
  computed: {
    secondName: {
      get () {
        return this.value.secondName
      },
      set (value) {
        this.emitFormData({ secondName: value })
      }
    },
    firstName: {
      get () {
        return this.value.firstName
      },
      set (value) {
        this.emitFormData({ firstName: value })
      }
    },
    patronymic: {
      get () {
        return this.value.patronymic
      },
      set (value) {
        this.emitFormData({ patronymic: value })
      }
    },
    gender: {
      get () {
        return this.value.gender
      },
      set (value) {
        this.emitFormData({ gender: value })
      }
    },
    birth_date: {
      get () {
        return this.value.birth_date
      },
      set (value) {
        this.emitFormData({ birth_date: value })
      }
    },
    die_date: {
      get () {
        return this.value.die_date
      },
      set (value) {
        this.emitFormData({ die_date: value })
      }
    },
    activity: {
      get () {
        return this.value.activity
      },
      set (value) {
        this.emitFormData({ activity: value })
      }
    },
    biography: {
      get () {
        return this.value.biography
      },
      set (value) {
        this.emitFormData({ biography: value })
      }
    }
  },
  methods: {
    emitFormData (param) {
      this.$emit('change', {
        ...this.value,
        ...param
      })
    }
  }
}
</script>

<style scoped lang="less">
.person-page {
  &__btn {
    justify-self: center;
    padding: 10px 20px;
    margin-top: 10px;
    border: none;
    border-radius: 5px;
    background-color: aqua;
    color: black;
    font-weight: 600;
    cursor: pointer;
    margin-left: 0px;
    margin-bottom: 20px;
  }
}
</style>
