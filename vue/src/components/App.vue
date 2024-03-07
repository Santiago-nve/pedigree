<template>
  <div>
    <RouterView />
    <ModalContainer />
  </div>
</template>

<script>
import ModalContainer from "@/components/parts/ModalContainer";

export default {
  components: {
    ModalContainer
  }
}
</script>

<style lang="less">
@import url('https://fonts.googleapis.com/css2?family=Jost:wght@400;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');

body {
  margin: 0;
  padding: 0;
  background-color: @cBaseTwo;
  font-family: @ffInter;
}

a {
  text-decoration: none;
}

section {
  background-color: @cBaseOne;
  margin-bottom: 20px;
  border-radius: 2px;
  box-sizing: border-box;

  &:last-child {
    margin-bottom: 0;
  }
}

h1, h2, h3, h4, h5 {
  font-family: @ffInter;
  color: @cBaseThree;
  margin: 0;
  margin-bottom: 8px;
}

h1 {
  font-size: 26px;
}

h2 {
  font-size: 20px;
}

h3 {
  font-size: 18px;
}

h4 {
  font-size: 16px;
}

.p-16 {
  padding: 16px;
}

.d-flex {
  display: flex;
}

.custom-form {
  width: 450px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 15px;
  margin-bottom: 15px;

  &__full-width {
    grid-column: span 2
  }

  &__input {

    &.el-date-editor {
      width: 100% !important;
    }

    & .el-input__inner {
      font-size: 14px;
      width: 100%;
      font-family: @ffInter;
    }

    & .el-textarea__inner {
      font-size: 14px;
      width: 100%;
      font-family: @ffInter;
      min-height: 100px !important;
    }
  }
}
</style>
