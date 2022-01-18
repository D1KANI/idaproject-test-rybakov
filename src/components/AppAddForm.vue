<template>
  <form class="add-form" @submit.prevent="addProduct()">
    <div class="input-wrapper">
      <label class="label">Наименование товара<span></span></label>
      <input
        v-model="nameProduct"
        @input="checkEmptyValue($event)"
        type="text"
        class="input"
        placeholder="Введите наименование товара"
      />
      <div class="input-error">Поле является обязательным</div>
    </div>
    <div class="input-wrapper">
      <label class="label">Описание товара</label>
      <textarea
        v-model="descProduct"
        class="input textarea"
        placeholder="Введите описание товара"
      ></textarea>
    </div>
    <div class="input-wrapper">
      <label class="label">Ссылка на изображение товара<span></span></label>
      <input
        v-model="imageLinkProduct"
        @input="checkEmptyValue($event)"
        type="text"
        class="input"
        placeholder="Введите ссылку"
      />
      <div class="input-error">Поле является обязательным</div>
    </div>
    <div class="input-wrapper">
      <label class="label">Цена товара<span></span></label>
      <input
        v-model="priceProduct"
        @input="checkEmptyValue($event, 'masked')"
        type="text"
        class="input"
        placeholder="Введите цену"
      />
      <div class="input-error">Поле является обязательным</div>
    </div>
    <button :class="classnameButton" class="btn">Добавить товар</button>
  </form>
</template>

<script>
export default {
  name: "AppAddForm",
  data() {
    return {
      lenghtAgreeInputs: 0,
      nameProduct: "",
      descProduct: "",
      imageLinkProduct: "",
      priceProduct: "",
    };
  },
  computed: {
    classnameButton() {
      if (!this.nameProduct || !this.imageLinkProduct || !this.priceProduct) {
        return "_disabled";
      } else {
        return "";
      }
    },
  },
  methods: {
    checkEmptyValue(e, modifier) {
      if (!e.target.value.length) {
        e.target.classList.add("_error");
        e.target.nextSibling.style.display = "block";
      } else {
        e.target.classList.remove("_error");
        e.target.nextSibling.style.display = "none";
      }
      if (modifier) {
        if (isNaN(e.target.value.replace(/\s/g, ''))) {
          this.priceProduct = '';
          this.checkEmptyValue(e);
        } else {
          this.priceProduct = String(this.priceProduct)
                            .replace(/\s/g, '')
                            .replace(/(\d)(?=(\d{3})+([^\d]|$))/g,"$1 ");
        }
      }
    },
    addProduct() {
      if (this.classnameButton === "") {
        let product = {
          name: this.nameProduct,
          desc: this.descProduct,
          image: this.imageLinkProduct,
          price: String(this.priceProduct).replace(
            /(\d)(?=(\d{3})+([^\d]|$))/g,
            "$1 "
          ),
        };
        this.$emit("add-product", product);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.add-form {
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  position: sticky;
  top: 24px;
}
.input {
  display: block;
  width: 100%;
  padding: 9px 15px 10px;
  border: none;
  border-radius: 4px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  font-family: "Source Sans Pro";
  font-size: 12px;
  line-height: 15px;
  border: 1px solid transparent;
  color: #3f3f3f;
  transition: border-color 175ms ease-out;
  &::placeholder {
    color: #b4b4b4;
  }
  &._error {
    border-color: #ff8484;
  }
  &-wrapper {
    width: 100%;
    margin-bottom: 16px;
  }
  &-error {
    display: none;
    font-size: 8px;
    line-height: 10px;
    letter-spacing: -0.02em;
    margin-top: 4px;
    color: #ff8484;
  }
}
.textarea {
  height: 108px;
  font-family: "Source Sans Pro";
  font-size: 12px;
  line-height: 15px;
  resize: none;
  &::placeholder {
    color: #b4b4b4;
  }
}
.label {
  display: block;
  width: max-content;
  margin-bottom: 4px;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  span {
    position: relative;
    &::before {
      content: "";
      display: block;
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background-color: #ff8484;
      position: absolute;
      top: 0;
      right: 0;
      transform: translateX(100%);
    }
  }
}
.btn {
  margin-top: 8px;
}
</style>
