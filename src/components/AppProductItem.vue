<template>
  <div class="product-item-wrapper">
    <a href="#" class="product-item">
      <img
        :src="image"
        alt="Product Image"
        class="product-item__image"
      />
      <div class="product-item__inner">
        <div class="product-item__name"><slot name="name"></slot></div>
        <div class="product-item__desc">
          <slot name="desc"></slot>
        </div>
        <div class="product-item__price"><slot name="price">10 000</slot> руб.</div>
      </div>
    </a>
    <div @click="deleteItem()" class="product-item__delete">
      <img src="../assets/images/delete.svg" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  name: "AppProductItem",
  props: {
    image: String
  },
  methods: {
    deleteItem() {
      this.$emit('delete-item', this.id_product);
    }
  }
};
</script>

<style lang="scss" scoped>
.product-item {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  &-wrapper {
    position: relative;
    &:hover {
      .product-item__delete {
        opacity: 1;
      }
    }
  }
  &__image {
    display: block;
    width: 100%;
    max-height: 200px;
    border-radius: 4px 4px 0px 0px;
    object-fit: cover;
  }
  &__inner {
    padding: 16px 16px 24px;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
  }
  &__name {
    margin-bottom: 16px;
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
  }
  &__desc {
    margin-bottom: 32px;
    font-size: 16px;
    line-height: 20px;
  }
  &__price {
    margin-top: auto;
    margin-bottom: 0;
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
  }
  &__delete {
    position: absolute;
    top: 0;
    right: 0;
    transform: translate(50%, -50%);
    width: 32px;
    height: 32px;
    border-radius: 10px;
    background: #FF8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 175ms ease-in-out;
    cursor: pointer;
  }
}



@media screen and (max-width: 1366px) { //Показываю кнопку удаления. Размер - ширина экрана ipad pro в горизонтали
  .product-item {
    &__delete {
      opacity: 1;
    }
  }
}
</style>
