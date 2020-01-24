<template>
  <div>
    <label>
      <slot />
      <sup>&ast;</sup>
    </label>

    <span v-for="(option, index) in options[0]" :key="index">
      <input :value="index" v-bind="$attrs" />
      {{option}}
    </span>
    <slot name="validation_message" />
  </div>
</template>

<script>
export default {
  name: "RadioInput",
  props: {
    options: {
      type: Array
    }
  }
};
</script>

<style scoped>
</style>