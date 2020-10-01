<template>
  <div class="custom-modal" :class="{ 'custom-modal-small': small }">
    <div class="custom-modal__container" :class="{'custom-modal__bg-img' : background}"
    >
      <div class="custom-modal__header">
        <span>{{ title }}</span>
        <a class="custom-modal__close" @click="close">
          &#x2716;
        </a>
      </div>
      <div class="custom-modal__body " ref="modal">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    title: { type: String, required: false, default: '' },
    background: { type: Boolean, required: false, default: false },
    small: { type: Boolean, required: false, default: false }
  },
  methods: {
    close() {
      this.$emit('close')
    }
  }
}
</script>

<style lang="scss" scoped>
.custom-modal {
  align-items: center;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  height: 100%;
  justify-content: center;
  left: 0;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  $p: &;
  &-small {
    #{$p}__container {
      width: 40% !important;
    }
    #{$p}__body {
      padding: 10px 0;
    }
  }
  &__bg-img{
    background: #d6027f url(../../assets/modal-bg.jpg) no-repeat center center / cover !important;
  }
  &__container {
    background: #fff;
    border-radius: 4px;
    box-shadow: (
      0 26px 26px 0 rgba(51, 51, 51, 0.14),
      0 0 1px 0 rgba(51, 51, 51, 0.12)
    );
    text-align: center;
    color: #fff;
    width: 65%;
  }
  &__header {
    align-items: center;
    display: flex;
    font-size: 20px;
    font-weight: 600;
    padding: 30px;
    position: relative;
  }
  &__close {
    &:hover {
      text-decoration: none;
    }
    color: #fff;
    opacity: 0.6;
    cursor: pointer;
    font-size: 24px;
    position: absolute;
    right: 8px;
    top: 5px;
  }
  &__body {
    padding: 60px 0;
    margin-bottom: 10px;
    max-height: 90%;
    overflow-y: auto;
    /deep/ img {
      width: 90%;
    }
  }

  &__pagination {
    padding: 30px;
  }

  &__footer {
    padding: 30px;
    text-align: right;
  }
}

@media (max-width: 767px) {
  .custom-modal {
    &__container {
      width: 90%;
    }
    &__body {
      padding: 40px 20px;
    }
    &__close {
      font-size: 24px;
    }
  }
}
</style>
