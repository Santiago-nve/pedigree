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
      v-model="patronymicName"
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
      v-model="birthDate"
      class="custom-form__input"
      type="date"
      format="dd.MM.yyyy"
      value-format="dd.MM.yyyy"
      placeholder="Дата рождения"
    />
    <ElDatePicker
      v-model="dieDate"
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
    <div class="custom-form__full-width">
      <ElSelect
        v-model="access"
        class="custom-form__input"
        placeholder="Скрывание">
        <ElOption
          label="Скрывать"
          value=true
        />
        <ElOption
          label="Не скрывать"
          value=false
        />
      </ElSelect>
    </div>
    
    <h2>Военная служба</h2>
    <div 
      class="custom-form__full-width" 
      v-for="(military, index) in value.militaries" 
      :key="'military' + index"
    >
      <div class ="person-page__header-wrapper">
      <h3>Военная служба {{ index + 1 }}</h3>
        <button class="person-page__btn-close" @click="() => removeMilitaryForm(index)">
          ✖
        </button>
      </div>
      <MilitaryForm
        :value="military"
        class="custom-form__input"
        @change="(military) => setMilitaryForm(military, index)"
      />
    </div>
    <div class ="custom-form__full-width person-page__right-wrapper">
      <SimpleButton type="primary" @click="() => addMilitaryForm()">
        Добавить
      </SimpleButton >
    </div>

    <h2>Брачные союзы</h2>
    <div 
      class="custom-form__full-width" 
      v-for="(wedding, index) in value.weddings" 
      :key="'wedding' + index"
    >
      <div class ="person-page__header-wrapper">
      <h2>Свадьба {{ index + 1 }}</h2>
        <button @click="() => removeWeddingForm(index)" class="person-page__btn-close ">
          ✖
        </button>
      </div>
      <WeddingForm
        :value="wedding" 
        :persons="partners"
        class="custom-form__input"
        @change="(wedding) => setWeddingForm(wedding, index)"
      />
    </div>
    <div class ="custom-form__full-width person-page__right-wrapper">
      <SimpleButton @click="() => addWeddingForm()" type="primary">
        Добавить 
      </SimpleButton >
    </div>

    <h2>Образование</h2>
    <div 
      class="custom-form__full-width" 
      v-for="(education, index) in value.educations" 
      :key="'education' + index"
    >
      <div class ="person-page__header-wrapper">
      <h2>Образование {{ index + 1 }}</h2>
        <button @click="() => removeEducationForm(index)" class="person-page__btn-close ">
          ✖
        </button>
      </div>
      <EducationForm
        :value="education"
        class="custom-form__input"
        @change="(education) => setEducationForm(education, index)"
      />
    </div>
    <div class ="custom-form__full-width person-page__right-wrapper">
      <SimpleButton @click="() => addEducationForm()" type="primary">
        Добавить 
      </SimpleButton >
    </div>

    <h2>Работа</h2>
    <div 
      class="custom-form__full-width" 
      v-for="(work, index) in value.works" 
      :key="'work' + index"
    >
      <div class ="person-page__header-wrapper">
      <h2>Работа {{ index + 1 }}</h2>
        <button @click="() => removeWorkForm(index)" class="person-page__btn-close ">
          ✖
        </button>
      </div>
      <WorkForm
        :value="work"
        class="custom-form__input"
        @change="(work) => setWorkForm(work, index)"
      />
    </div>
    <div class ="custom-form__full-width person-page__right-wrapper">
      <SimpleButton @click="() => addWorkForm()" type="primary">
        Добавить
      </SimpleButton >
    </div>

    <h2>Дети</h2>
    <div 
      class="custom-form__full-width" 
      v-for="(child, index) in value.children" 
      :key="'child' + index"
    >
      <div class ="person-page__header-wrapper">
      <h2>Ребёнок {{ index + 1 }}</h2>
        <button @click="() => removeChildForm(index)" class="person-page__btn-close ">
          ✖
        </button>
      </div>
      <ChildForm
        :value="child" 
        :persons="childrens"
        class="custom-form__input"
        @change="(child) => setChildForm(child, index)"
      />
    </div>
    <div class ="custom-form__full-width person-page__right-wrapper">
      <SimpleButton @click="() => addChildForm()" type="primary">
        Добавить 
      </SimpleButton >
    </div>
  </div>
</template>

<script>
import MilitaryForm from '../forms/MilitaryForm.vue'
import SimpleButton from '../ui/SimpleButton.vue'
import WeddingForm from '../forms/WeddingForm.vue'
import ChildForm from '../forms/ChildForm.vue'
import { mapGetters } from 'vuex'
import EducationForm from '../forms/EducationForm.vue'
import WorkForm from '../forms/WorkForm.vue'
import { emptyWedding, emptyWork, emptyMilitary, emptyEducation } from '@/services/person'

export default {
  name: 'PersonForm',
  model: {
    prop: 'value',
    event: 'change'
  },
  components: {
    WorkForm,
    EducationForm,
    WeddingForm,
    ChildForm,
    MilitaryForm,
    SimpleButton
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
    patronymicName: {
      get () {
        return this.value.patronymicName
      },
      set (value) {
        this.emitFormData({ patronymicName: value })
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
    birthDate: {
      get () {
        return this.value.birthDate
      },
      set (value) {
        this.emitFormData({ birthDate: value })
      }
    },
    dieDate: {
      get () {
        return this.value.dieDate
      },
      set (value) {
        this.emitFormData({ dieDate: value })
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
    },
    access: {
      get () {
        if (this.value.access) {
          return 'true'
        }
        else {
          return 'false'
        }
      },
      set (value) {
        if (value == 'true') {
          value = true
        }
        else {
          value = false
        }
        this.emitFormData({
          access: value
        })
      }
    },

    ...mapGetters ('persons', [
      'filteredPersons',
      'getAllPersons',
      'getPersonById',
      'getCenter'
    ]),
    id () {
      return this.$route.params.id
    },
    person () {
      return this.getPersonById(this.id)
    },
    partners () {
      const customFilter = (person) => {
        const partnerBirthDate = this.formatDate(person.birthDate)
        const partnerDeathDate = this.formatDate(person.dieDate)
        const deathDate = this.formatDate(this.value.dieDate)
        const birthDate = this.formatDate(this.value.birthDate)
        return (
          this.value.gender !== person.gender &&
          (!this.value.dieDate || !person.birthDate || deathDate > partnerBirthDate) &&
          (!this.value.birthDate || !person.dieDate || birthDate < partnerDeathDate)
        )
      }
      return this.filteredPersons(customFilter) || []
    },
    childrens () {
      const customFilter = (person) => {
        const childBirthDate = this.formatDate(person.birthDate)
        const childDeathDate = this.formatDate(person.dieDate)
        const deathDate = this.formatDate(this.value.dieDate)
        const birthDate = this.formatDate(this.value.birthDate)
        return (
          birthDate > childBirthDate &&
          (!this.value.dieDate || !person.birthDate || deathDate > childBirthDate) &&
          (!this.value.birthDate || !person.dieDate || birthDate < childDeathDate)
        )
      }
      return this.filteredPersons(customFilter) || []
    }
  },
  methods: {
    emitFormData (param) {
      this.$emit('change', {
        ...this.value,
        ...param
      })
    },
    formatDate(date) {
      if (date) {
        const getYear = parseInt(date.slice(6,10))
        const getMonth = parseInt(date.slice(3,5))
        const getDay = parseInt(date.slice(0,2))
        return new Date(getYear, getMonth, getDay)
      }
      return null
    },

    setMilitaryForm (updatedMilitary, index) {
      const newValue = { ...this.value }
      newValue.militaries[index] = updatedMilitary
      newValue.militaries = [...newValue.militaries]
      this.$emit('change', newValue)
    },
    addMilitaryForm () {
      const newValue = { ...this.value }
      newValue.militaries.push(emptyMilitary())
      this.$emit('change', newValue)
    },
    removeMilitaryForm (index) {
      const newValue = { ...this.value }
      newValue.militaries.splice(index, 1)
      this.$emit('change', newValue)
    },

    setWeddingForm (updatedWedding, index) {
      const newValue = { ...this.value }
      newValue.weddings = [...newValue.weddings]
      newValue.weddings[index] = updatedWedding
      this.$emit('change', newValue)
    },
    addWeddingForm () {
      const newValue = { ...this.value }
      newValue.weddings.push(emptyWedding())
      this.$emit('change', newValue)
    },
    removeWeddingForm (index) {
      const newValue = { ...this.value }
      newValue.weddings.splice(index, 1)
      this.$emit('change', newValue)
    },

    setChildForm (updatedChild, index) {
      const newValue = { ...this.value }
      newValue.children = [...newValue.children]
      newValue.children[index] = updatedChild
      this.$emit('change', newValue)
    },
    addChildForm () {
      const newValue = { ...this.value }
      newValue.children.push({ child: '' })
      this.$emit('change', newValue)
    },
    removeChildForm (index) {
      const newValue = { ...this.value }
      newValue.children.splice(index, 1)
      this.$emit('change', newValue)
    },
    
    setEducationForm (updatedEducation, index) {
      const newValue = { ...this.value }
      newValue.educations = [...newValue.educations]
      newValue.educations[index] = updatedEducation
      this.$emit('change', newValue)
    },
    addEducationForm () {
      const newValue = { ...this.value }
      newValue.educations.push(emptyEducation())
      this.$emit('change', newValue)
    },
    removeEducationForm (index) {
      const newValue = { ...this.value }
      newValue.educations.splice(index, 1)
      this.$emit('change', newValue)
    },

    setWorkForm (updatedWork, index) {
      const newValue = { ...this.value }
      newValue.works = [...newValue.works]
      newValue.works[index] = updatedWork
      this.$emit('change', newValue)
    },
    addWorkForm () {
      const newValue = { ...this.value }
      newValue.works.push(emptyWork())
      this.$emit('change', newValue)
    },
    removeWorkForm (index) {
      const newValue = { ...this.value }
      newValue.works.splice(index, 1)
      this.$emit('change', newValue)
    }
  }
}
</script>

<style scoped lang="less">
@media (max-width: 720px) {
  .custom-form {
    display: flex;
    width: 100%;
    flex-direction: column;
  }
} 

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

  &__btn-close {
    background: none;
    border: none;
    cursor: pointer;
  }

  &__header-wrapper {
    display: grid;
    grid-template-columns: auto max-content;
  }

  &__right-wrapper {
    text-align: right;
  }
}
</style>
