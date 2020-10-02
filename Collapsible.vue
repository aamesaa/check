<template>
  <div class="collapsible__item">
    <div
      class="dropdown"
      ref="dropdown-ingredients"
      @click="dropdown('dropdown-ingredients')"
    >
      <div class="item__title">{{ label }}</div>
      <div class="item__desc">
        <div class="dropdown__placeholder ingredient">
          {{ placeholder }}
        </div>
        <div class="dropdown__list" :class="['active']">
          <div class="dropdown__item">
            {{ content }}
          </div>
        </div>
      </div>
      <div class="dropdown__img">
        <img src="@assets/dropdown.png" alt="dropdown" />
      </div>
    </div>
  </div>
</template>

<script>
import DropdownMixins from '@/mixins/DropdownMixins'
export default {
  name: 'Collapsible',
  mixins: [DropdownMixins],
  props: {
    label: { type: String, required: false, default: '' },
    placeholder: { type: String, required: false, default: '' },
    content: { type: String, required: false, default: '' }
  }
}
</script>

<style lang="scss" scoped>
$transition: 0.5s ease-out;
* {
  box-sizing: border-box;
  transition: $transition;
}
.item {
  &__title {
    flex-basis: 55%;
    text-align: left;
    font-size: 32px;
    width: 30vw;
    font-weight: 600;
  }
  &__desc {
    flex-basis: 45%;
    width: 15vw;
    margin-left: 20px;
    margin-right: 10px;
    color: #808080;
    font-size: 18px;
  }
}
.collapsible {
  &__description {
    margin: auto 10vw;
    width: 50vw;
  }
  &__item {
    display: flex;
    font-size: 14px;
    padding: 20px;
    font-weight: 300;
  }
}
.button {
  margin-top: 20px;
}
@media (max-width: 103px) {
  .item {
    &__desc {
      font-size: 18px;
      width: 50vw;
    }
  }
  .collapsible {
    &__item {
      padding: 20px 0;
      font-size: 18px;
    }
  }
}
@media (max-width: 767px) {
  .dropdown {
    display: flex;
    flex-wrap: wrap;
    &__img {
      margin-left: unset;
      position: absolute;
      right: 0;
      top: 16px;
    }
  }
  .collapsible {
    &__description {
      width: 100%;
      margin-left: 0;
    }
    &__item {
      display: flex;
      font-size: 20px;
      padding: 10px 0;
    }
  }
  .item {
    &__title {
      font-size: 20px;
      padding: 14px 0;
      flex-basis: 95%;
    }
    &__desc {
      width: 100%;
      flex-basis: 100%;
      margin-left: 0;
    }
  }
}
</style>
