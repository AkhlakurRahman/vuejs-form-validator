<template>
  <div class="multiselect-input">
    <label :for="multiSelectInput.name">
      {{ multiSelectInput.label }}
      <sup>&ast;</sup>
    </label>

    <select
      :name="multiSelectInput.name"
      :id="multiSelectInput.name"
      @change="onMultiSelectChangeHandler"
      v-model="multiSelectInputValue"
      multiple
    >
      <option value="default">----Select your suitable occupation(s)----</option>
      <option
        v-for="(option, index) in multiSelectInput.options[0]"
        :value="index"
        :key="index"
      >{{ option }}</option>
    </select>

    <span
      :class="(!inputError && multiSelectInputValue.length <=0 || multiSelectInputValue.length !== 0) ? 'd-none' : null"
    >{{ multiSelectInput.validation_message }}</span>
  </div>
</template>

<script>
export default {
  name: "MultiSelect",
  props: {
    multiSelectInput: {
      type: Object
    },
    inputError: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      multiSelectInputValue: []
    };
  },
  methods: {
    onMultiSelectChangeHandler: function() {
      this.$emit("onMultiSelectChangeHandler", this.multiSelectInputValue);
    }
  }
};
</script>

<style lang="scss" scoped>
.multiselect-input {
  width: 40rem;

  select {
    color: rgb(70, 71, 75);
  }
}
</style>
