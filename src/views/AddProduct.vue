<template>
  <section class="add-product-page">
    <div class="container">
      <div class="add-product-head">
        <h1>Добавление товара</h1>
        <app-sort-btn
          @sort-decrease="sortProductsIncreaseByPrice()"
          @sort-increase="sortProductsDecreaseByPrice()"
          @sort-default="sortProductsByName()"
        ></app-sort-btn>
      </div>
      <div class="add-product-body">
        <div class="add-product-form">
          <app-add-form @add-product="addProduct($event)"></app-add-form>
        </div>
        <transition name="fade" mode="out-in">
        <transition-group name="fade" tag="div" class="add-product-content" v-if="products.length">
          <div
            v-for="(item, index) in products"
            :key="index"
            class="add-product-item"
          >
            <app-product-item
              @delete-item="deleteItem(index)"
              :image="item.image"
            >
              <template v-slot:name>
                {{ item.name }}
              </template>
              <template v-slot:desc>
                {{ item.desc }}
              </template>
              <template v-slot:price>
                {{ item.price }}
              </template>
            </app-product-item>
          </div>
        </transition-group>
        <div class="add-product-content-empty" v-else>
          Список пуст, пожалуйста, добавьте товары
        </div>
        </transition>
      </div>
    </div>
  </section>
</template>

<script>
import AppSortBtn from "@/components/AppSortBtn.vue";
import AppAddForm from "@/components/AppAddForm.vue";
import AppProductItem from "@/components/AppProductItem.vue";
import productImageDefault from "../assets/images/productImageExample.png";

export default {
  name: "AddProduct",
  components: {
    AppSortBtn,
    AppAddForm,
    AppProductItem,
  },
  data() {
    return {
      products: [], // Сделал для примера, так как по сути должен быть запрос на получение объекта с сервера. Само собой тогда и удаление будет по полю ID от бэка.
    };
  },
  methods: {
    deleteItem(index) {
      this.products.splice(index, 1);
      localStorage.setItem("products", JSON.stringify(this.products));
    },
    addProduct(product) {
      this.products.push(product);
      localStorage.setItem("products", JSON.stringify(this.products));
    },
    sortProductsByName() {
      this.products.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
    sortProductsIncreaseByPrice() {
      this.products.sort((a, b) => +a.price < +b.price ? 1 : -1);
    },
    sortProductsDecreaseByPrice() {
      this.products.sort((a, b) => +a.price.replace(/\s/g, '') > +b.price.replace(/\s/g, '') ? 1 : -1);
      // this.products.sort((a, b) => console.log(+a.price.replace(/\s/g, '')));
    },
  },
  beforeMount() {
    if (localStorage.getItem("products")) {
      this.products = JSON.parse(localStorage.getItem("products"));
    } else {
      this.products = [
        {
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
          image: productImageDefault
        },
        {
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
          image: productImageDefault
        },
        {
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
          image: productImageDefault
        }
      ];
      localStorage.setItem("products", JSON.stringify(this.products));
    }
  },
};
</script>

<style scoped lang="scss">
.add-product {
  &-page {
    padding: 32px 0;
  }
  &-head {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 16px;
  }
  &-body {
    display: flex;
  }
  &-form {
    min-height: 100%;
    min-width: 332px;
    margin-right: 16px;
  }
  &-content {
    display: flex;
    justify-content: flex-start;
    align-items: stretch;
    flex-wrap: wrap;
    margin: 0 -8px;
    flex-grow: 1;
    &-empty {
      font-size: 24px;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
  &-item {
    width: calc(100% / 3 - 16px);
    margin: 0 8px 16px;
  }
}

@media screen and (max-width:1230px) {
  .add-product {
    &-item {
      width: calc(100% / 2 - 16px);
    }
  }
}

@media screen and (max-width: 990px) {
  .add-product {
    &-item {
      width: calc(100% - 16px);
    }
  }
}

@media screen and (max-width: 680px) {
  .add-product {
    &-body {
      display: block;
    }
    &-form {
      margin-right: 0;
      margin-bottom: 24px;
    }
  }
}

@media screen and (max-width: 480px) {
  .add-product {
    &-head {
      display: block;
      h1 {
        margin-bottom: 16px;
      }
    }
    &-form {
      min-width: 1px;
    }
  }
}

.fade-enter-active, .fade-leave-active {
  transition: all 250ms;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
