<template>
  <div class="photo-preview">
    <img
      class="photo-preview__img"
      :class="'photo-preview__img--' + size"
      :src="imageSource"
      alt="Фото"
    >
  </div>
</template>

<script>
export default {
  name: 'PhotoPreview',
  props: {
    photo: {
      default: '',
      type: String
    },
    size: {
      default: 'middle',
      type: String
    }
  },
  computed: {
    imageSource () {
      return this.photo || require('@/assets/photo-default.jpg');
    }
  }
}
</script>

<style scoped lang="less">
.photo-preview {

  &__img {
    object-fit: cover;
    border-radius: 12px;

    &--large {
      width: 200px;
      height: 300px;
    }

    &--middle {
      width: 150px;
      height: 200px;
    }

    &--small {
      width: 80px;
      height: 120px;
    }
  }
}
</style>
