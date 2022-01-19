<template>
  
    <div class="input-wrapper">
      <label class="label">{{ label }}<span v-if="required"></span></label>
      <textarea
        v-if="type === 'textarea'"
        class="input textarea"
        :placeholder="placeholder"
        :value="value"
        :name="name"
      ></textarea>
      <input
        v-else
        @input="checkEmptyValue($event)"
        type="text"
        class="input"
        placeholder="Введите ссылку"
        :value="value"
        :name="name"
      />
      <div v-if="!validation" class="input-error">Поле является обязательным</div>
    </div>
</template>
<script>

export default ({
  name: 'AppInput',
  props: {
    label: String,
    placeholder: String,
    required: {
      type: Boolean,
      default: false
    },
    type: String,
    value: String,
    modifier: String,
    name: String
  },
  data() {
    return {
      validation: true
    }
  },
  methods: {
    checkEmptyValue(e) {
      if (!e.target.value.length) {
        e.target.classList.add("_error");
        this.validation = false;
      } else {
        e.target.classList.remove("_error");
        this.validation = true;
      }
      if (this.modifier) {
        if (isNaN(e.target.value.replace(/\s/g, ''))) {
          e.target.value = '';
          this.checkEmptyValue(e);
        } else {
          e.target.value = String(e.target.value)
                            .replace(/\s/g, '')
                            .replace(/(\d)(?=(\d{3})+([^\d]|$))/g,"$1 ");
        }
      }
      this.$emit('input', e.target.value);
    },
  }
})
</script>
<style lang="scss" scoped>

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
</style>