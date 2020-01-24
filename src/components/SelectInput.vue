<template>
  <div class="select-input">
    <label :for="singleSelect.name">
      {{singleSelect.label}}
      <sup>&ast;</sup>
    </label>

    <select
      :name="singleSelect.name"
      :id="singleSelect.name"
      @change="onSelectChangeHandler"
      v-model="selectInputValue"
    >
      <option value="default">Select a status</option>
      <option
        v-for="(option, index) in singleSelect.options[0]"
        :value="index"
        :key="index"
      >{{ option }}</option>
    </select>

    <span
      :class="(!inputError && selectInputValue === 'default' || selectInputValue !== 'default') ? 'd-none' : null"
    >{{singleSelect.validation_message}}</span>
  </div>
</template>

<script>
export default {
  name: "SelectInput",
  props: {
    singleSelect: {
      type: Object
    },
    inputError: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      selectInputValue: "default"
    };
  },
  methods: {
    onSelectChangeHandler: function() {
      this.$emit("onSelectChangeHandler", this.selectInputValue);
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
