<template>
  <div class="form-input">
    <label :for="focusAttribute">
      <slot />
      <sup>&ast;</sup>
    </label>

    <input v-bind="$attrs" :id="focusAttribute" :value="value" />

    <slot name="validation_message" />
  </div>
</template>

<script>
export default {
  name: "FormInput",
  props: {
    value: {
      type: String,
      default: ""
    },
    focusAttribute: {
      type: String
    }
  }
};
</script>

<style lang="scss" scoped>
.form-input {
  width: 40rem;

  input::placeholder {
    font-family: "Fira Sans", sans-serif;
    color: rgb(118, 120, 128);
    font-size: 1.6rem;
  }
}
</style>
