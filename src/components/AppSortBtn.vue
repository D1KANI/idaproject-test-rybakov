<template>
  <div class="sort-btn">
    <div
      @click="showContent = !showContent"
      :class="classnameHead"
      class="sort-btn-head"
    >
      {{ activeText }}
    </div>
    <transition
      name="fade"
    >
      <div class="sort-btn-body" v-if="showContent">
        <div @click="changeSort($event, 'byName')" class="sort-btn-body__item">
          По названию
        </div>
        <div @click="changeSort($event, 'increase')" class="sort-btn-body__item">
          Сначала дешевые
        </div>
        <div @click="changeSort($event, 'decrease')" class="sort-btn-body__item">
          Сначала дорогие
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
export default {
  name: "AppSortBtn",
  data() {
    return {
      showContent: false,
      activeText: "По умолчанию",
    };
  },
  computed: {
    classnameHead() {
      if (this.showContent) {
        return "_active";
      } else {
        return "";
      }
    },
  },
  methods: {
    changeSort(e, status) {
      this.activeText = e.target.innerText;
      if (status === 'increase') {
        this.$emit('sort-increase');
      } else if (status === 'decrease') {
        this.$emit('sort-decrease');
      } else if (status === 'byName') {
        this.$emit('sort-default');
      }
    },
  },
};
</script>
<style lang="scss" scoped>
$gray: #b4b4b4;
.sort-btn {
  position: relative;
  width: 140px; // Сделал фиксированно, чтобы ширина не увеличивалась/уменьшалась
  &-head {
    position: relative;
    z-index: 3;
    padding: 10px 29px 11px 16px;
    border-radius: 4px;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    font-size: 12px;
    line-height: 15px;
    color: $gray;
    cursor: pointer;
    user-select: none;
    &::before,
    &::after {
      content: "";
      display: block;
      width: 5px;
      height: 2px;
      background-color: $gray;
      position: absolute;
      top: 50%;
      right: 19px;
      transition: all 175ms ease-out;
    }
    &::before {
      transform: translateY(-50%) rotate(45deg);
    }
    &:after {
      transform: translate(calc(100% - 2px), -50%) rotate(-45deg);
    }
    &._active {
      &::before {
        transform: translateY(-50%) rotate(-45deg);
      }
      &::after {
        transform: translate(calc(100% - 2px), -50%) rotate(45deg);
      }
    }
  }
  &-body {
    width: 100%;
    position: absolute;
    top: calc(100% + 4px);
    z-index: 2;
    border-radius: 4px;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    transition: opacity 175ms ease-out;
    &__item {
      margin: 0 10px;
      padding: 5px 0;
      font-size: 12px;
      color: $gray;
      cursor: pointer;
      transition: color 175ms ease-out;
      &:hover {
        color: #3f3f3f;
      }
    }
  }
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
.fade-enter-to, .fade-leave {
  opacity: 1;
}
</style>
