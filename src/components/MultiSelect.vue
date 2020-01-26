<template>
  <div class="multiselect-input">
    <label :for="multiSelectInput.name">
      {{ multiSelectInput.label }}
      <sup>&ast;</sup>
    </label>

    <select
      :name="multiSelectInput.name"
      :id="multiSelectInput.name"
      v-model="multiSelectInputValue"
      @change="onInputChange"
      :required="multiSelectInput.required"
      multiple
    >
      <option value="default" disabled selected>----{{multiSelectInput.placeholder}}(s)----</option>
      <option
        v-for="(option, index) in multiSelectInput.options[0]"
        :value="index"
        :key="index"
      >{{ option }}</option>
    </select>

    <span
      :class="{dnone: !isInputFieldEmpty && isInputFieldRequired || !isInputFieldRequired}"
    >{{ multiSelectInput.validation_message }}</span>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "MultiSelect",
  props: {
    multiSelectInput: {
      type: Object
    }
  },
  data() {
    return {
      multiSelectInputValue: [],
      isInputFieldRequired: this.multiSelectInput.required,
      isInputFieldEmpty: false
    };
  },
  methods: {
    onInputChange: function() {
      if (this.multiSelectInputValue.length === 0) {
        this.isInputFieldEmpty = true;
      } else {
        this.isInputFieldEmpty = false;
      }
    },
    checkIfRequiredFieldEmpty: function() {
      return (
        this.multiSelectInput.required &&
        this.multiSelectInputValue.length === 0
      );
    }
  },
  created() {
    eventBus.$on("onSubmitHandler", () => {
      this.onInputChange();

      if (!this.isInputFieldEmpty && !this.checkIfRequiredFieldEmpty()) {
        eventBus.$emit("onSuccesSubmission", {
          [this.multiSelectInput.label]: this.multiSelectInputValue
        });
        this.multiSelectInputValue = "";
        this.isInputFieldEmpty = false;
      }
    });
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
