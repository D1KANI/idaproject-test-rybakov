<template>
  <div class="input-wrapper">
    <label class="label">{{ label }}<span v-if="required"></span></label>
    <template v-if="inputType === 'input'">
      <input @input="checkEmptyValue($event)" type="text" class="input" :placeholder="placeholder" />
    </template>
    <template v-if="inputType === 'textarea'">
      <textarea class="input textarea" :placeholder="placeholder"></textarea>
    </template>
  </div>
</template>

<script>
export default {
  name: "BaseInput",
  props: {
    label: String,
    placeholder: String,
    type: String,
    required: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    inputType() {
      if (this.type) {
        if (this.type === "textarea") {
          return "textarea";
        } else {
          return "input";
        }
      } else {
        return "input";
      }
    },
  },
  methods: {
    checkEmptyValue(e) {
      if (!e.target.value.length) {
        e.target.classList.add('_error');
      } else {
        e.target.classList.remove('_error');
      }
    }
  }
};
</script>

<style lang="scss" scoped>

</style>
