<template>
  <form :class="{ 'has-value': !!localValue }" @submit.prevent="">
    <div v-if="type === 'checkbox'" class="cb" @click="clickCb">
      <input
        :checked="localValue"
        v-model="localValue"
        type="checkbox"
        :id="localId"
        :name="name"
      />
      <label :for="localId">{{ label }}</label>
    </div>
    <div v-else>
      <input
        class="input"
        v-model="localValue"
        :type="type"
        :name="name"
        :id="localId"
        :class="{ invalid: !valid }"
        :disabled="disabled"
      />
      <label :for="localId">{{ label }}</label>
      <span v-if="!valid" class="invalid-text">{{ errorMsg }}</span>
    </div>
  </form>
</template>
<script>
import { $uuid } from '@helper'

export default {
  name: 'I-Input',
  data() {
    return {
      localValue: this.value
    }
  },
  props: {
    label: { type: String, required: true, default: 'LABEL' },
    type: { type: String, required: true, default: 'text' },
    name: { type: String, required: false, default: 'text' },
    valid: { type: Boolean, required: false, default: true },
    disabled: { type: Boolean, required: false, default: false },
    errorMsg: { type: String, required: false },
    id: String,
    value: undefined,
    optValue: undefined
  },
  methods: {
    clickCb() {
      this.$emit('input', !this.localValue)
      this.localValue = !this.localValue
    }
  },
  computed: {
    localId() {
      return this.id || $uuid.generate
    }
  },
  watch: {
    localValue: {
      handler() {
        this.$emit('input', this.localValue)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
label{
  font-weight: normal;
}
$speed: 0.5s;

.cb {
  height: 2em;
}

form {
  width: 100%;
  float: left;
  // margin: 20px;
  > div {
    position: relative;
    overflow: hidden;
  }
  input[type='text'],
  input[type='number'],
  input[type='password'],
  textarea {
    color: #848484;
    width: 100%;
    border: none;
    font-size: 24px;
    border-bottom: 1px solid #808080;
    background: none;
    position: relative;
    margin-top: 20px;
    left: 0;
    z-index: 1;
    padding: 2px 10px;
    outline: 0;
  }

  label {
    margin-top: 20px;
    transition: background $speed, color $speed, top $speed, padding $speed,
      bottom $speed, right $speed, left $speed, font-size $speed;
    position: absolute;
    color: #999;
    padding: 7px 6px;
    bottom: 0;
    left: 0;
    top: 0;
    text-transform: capitalize;
    width: 100%;
  }
}

input[type='text'],
input[type='number'],
input[type='password'],
textarea {
  &:focus {
    border-color: #000;
    background: transparent;
    padding: 20px 6px 4px 1px;
    margin-top: 0;
  }

  &:focus + label {
    font-size: 70% !important;
    padding: 0;
    z-index: 2;
    top: -15px;
    bottom: 100%;
    margin-bottom: -16px;
    transition: background $speed, color $speed, top $speed, padding $speed,
      bottom $speed, right $speed, left $speed font-size $speed;
  }
  &:disabled {
    cursor: not-allowed;
    background-color: rgba(248, 248, 248, 0.35);
  }
}

.invalid,
input:focus.invalid {
  border-color: red;

  &-text {
    font-size: 12px;
    color: red;
    background: transparent;
  }
}

.go-bottom {
  input,
  textarea {
    background: transparent;
    & + label {
      display: none;
    }
  }
}

</style>
