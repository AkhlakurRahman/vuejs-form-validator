<template>
  <div class="select-input">
    <label :for="singleSelect.name">
      {{singleSelect.label}}
      <sup>&ast;</sup>
    </label>

    <select
      :name="singleSelect.name"
      :id="singleSelect.name"
      v-model="selectInputValue"
      :required="singleSelect.required"
      @change="onInputChange"
    >
      <option value="default" disabled selected>Select a status</option>
      <option
        v-for="(option, index) in singleSelect.options[0]"
        :value="index"
        :key="index"
      >{{ option }}</option>
    </select>

    <span
      :class="{dnone: !isInputFieldEmpty && isInputFieldRequired || !isInputFieldRequired}"
    >{{singleSelect.validation_message}}</span>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "SelectInput",
  props: {
    singleSelect: {
      type: Object
    }
  },
  data() {
    return {
      selectInputValue: "default",
      isInputFieldRequired: this.singleSelect.required,
      isInputFieldEmpty: false
    };
  },
  methods: {
    onInputChange: function() {
      if (this.selectInputValue === "default") {
        this.isInputFieldEmpty = true;
      } else {
        this.isInputFieldEmpty = false;
      }
    },

    checkIfRequiredFieldEmpty: function() {
      return this.singleSelect.required && this.selectInputValue === "default";
    }
  },
  created() {
    eventBus.$on("onSubmitHandler", () => {
      this.onInputChange();

      if (this.checkIfRequiredFieldEmpty()) {
        eventBus.$emit("passedAllValidation", false);
      }

      if (!this.isInputFieldEmpty && !this.checkIfRequiredFieldEmpty()) {
        eventBus.$emit("onSuccesSubmission", {
          [this.singleSelect.label]: this.selectInputValue
        });
        this.selectInputValue = "default";
        this.isInputFieldEmpty = false;
      }
    });
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
