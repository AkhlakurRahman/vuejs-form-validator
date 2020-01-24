<template>
  <div class="select-input">
    <label for>
      <slot />
      <sup>&ast;</sup>
    </label>
    <select :name="name">
      <option value="default">Select an status</option>
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
    color: rgb(70, 71, 75);
    font-size: 1.6rem;
    font-family: "Fira Sans", sans-serif;

    option {
      font-weight: 400;
    }
  }
}
</style>
