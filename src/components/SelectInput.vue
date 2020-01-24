<template>
  <div class="select-input">
    <label for>
      <slot />
      <sup>&ast;</sup>
    </label>
    <select :name="name">
      <option v-for="(option, index) in options[0]" :value="index" :key="index">{{ option }}</option>
    </select>
    <slot name="validation_message" />
  </div>
</template>

<script>
export default {
  name: "SelectInput",
  props: {
    name: {
      type: String,
      default: "select_input"
    },
    options: {
      type: Array
    }
  }
};
</script>

<style lang="scss" scoped>
.select-input {
  width: 40rem;

  select {
  }
}
</style>
