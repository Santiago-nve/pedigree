<template>
  <div class="navigation-panel">
    <RouterLink to="/settings">
      <SimpleButton type="info">Настройки</SimpleButton>
    </RouterLink>
    <RouterLink to="/">
      <SimpleButton type="warning">В центр</SimpleButton>
    </RouterLink>
    <RouterLink to="/">
      <SimpleButton type="danger">Удалить</SimpleButton>
    </RouterLink>
    <RouterLink to="/create">
      <SimpleButton type="primary">Добавить</SimpleButton>
    </RouterLink>
  </div>
</template>

<script>
import SimpleButton from "./SimpleButton.vue";

export default {
  components: {
    SimpleButton,
  },
};
</script>

<style scoped>
.navigation-panel {
  display: flex;
  justify-content: space-between;
  font-family: "Montserrat", sans-serif;
  padding: 10px;
}

.navigation-panel .simple-button {
  flex: 1;
  color: #000000c7;
  font-weight: 800;
}

.navigation-panel a {
  flex: 1;
  display: flex;
  margin-right: 10px;
}

.navigation-panel a:last-child {
  margin-right: 0;
}
</style>
