<template>
  <form class="add-form" id="addProductForm" @submit.prevent="addProduct()">
    <app-input
      v-for="(item, index) in inputs"
      :key="index"
      :label="item.label"
      :placeholder="item.placeholder"
      :required="item.required"
      :type="item.type"
      v-model="item.value"
      :modifier="item.modifier"
      :name="item.name"
      >
    </app-input>
    <button :class="classnameButton" class="btn">Добавить товар</button>
  </form>
</template>

<script>
import AppInput from '@/components/AppInput.vue'
export default {
  name: "AppAddForm",
  components: {
    AppInput,
  },
  data() {
    return {
      inputs: [
        {
          type: 'input',
          label: 'Наименование товара',
          placeholder: 'Введите наименование товара',
          value: '',
          required: true,
          modifier: '',
          name: 'name'
        },
        {
          type: 'textarea',
          label: 'Описание товара',
          placeholder: 'Введите описание товара',
          value: '',
          required: false,
          modifier: '',
          name: 'desc'
        },
        {
          type: 'input',
          label: 'Ссылка на изображение товара',
          placeholder: 'Введите ссылку',
          value: '',
          required: true,
          modifier: '',
          name: 'image'
        },
        {
          type: 'input',
          label: 'Цена товара',
          placeholder: 'Введите цену',
          value: '',
          required: true,
          modifier: 'price',
          name: 'price'
        },
      ],
    };
  },
  computed: {
    classnameButton() {
      let countRequired = 0,
          countInputSuccess = 0;
      this.inputs.forEach(input => {
        if (input.required) {
          countRequired++;
          if (input.value.length) {
            countInputSuccess++;
          }
        }
      });
      if (countRequired != countInputSuccess) {
        return "_disabled";
      } else {
        return "";
      }
    },
  },
  methods: {
    addProduct() {
      if (this.classnameButton === "") {
        let form = document.forms.addProductForm;
        let product = {
          name: form.elements.name.value,
          desc: form.elements.desc.value,
          image: form.elements.image.value,
          price: String(form.elements.price.value).replace(
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
.btn {
  margin-top: 8px;
}
</style>
