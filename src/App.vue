<template>
  <div class="page-wrapper">
    <div id="app">
      <add-product></add-product>
    </div>
  </div>
</template>

<script>
import AddProduct from '@/views/AddProduct.vue';

export default {
  name: 'App',
  components: {
    AddProduct,
  }
}
</script>

<style lang="scss">
// Все шрифты ковертированы в BASE64 для более быстрой загрузки
@import url(./assets/fonts/SourceSansPro/stylesheet.css);
@import url(./assets/fonts/Inter/stylesheet.css); // Добавил сразу на весь проект, для возможного расширения проекта.

$colorText: #3F3F3F;

// Обнуление стилей браузера, а также глобальные стили
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: #FAF9F7;
  font-family: "Source Sans Pro";
  color: $colorText;
}

a {
  text-decoration: none;
  color: inherit;
}

img {
  pointer-events: none;
  user-select: none;
}

input,
textarea,
button {
  outline: none;
}

.page-wrapper {
  min-height: 100vh;
}

.container {
  width: 1440px;
  max-width: 100%;
  margin: 0 auto;
  padding: 0 32px;
}

h1 {
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
}

.btn {
  width: 100%;
  padding: 10px 16px;
  border: none;
  border-radius: 10px;
  background: #7bae73;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  color: #fff;
  text-align: center;
  font-family: "Inter";
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  letter-spacing: -0.02em;
  cursor: pointer;
  transition: 175ms ease-out;
  &._disabled {
    background: #EEEEEE;
    color: #B4B4B4;
    cursor: not-allowed;
  }
}

.animated {
  animation-duration: 450ms;
}

</style>
