<template>
  <div>
    <div class="form-input">
      <label :for="textField.name">
        {{textField.label}}
        <sup>&ast;</sup>
      </label>

      <input
        :type="textField.type"
        :placeholder="textField.placeholder"
        :name="textField.name"
        :id="textField.name"
        v-model="inputTextValue"
        :required="textField.required"
        @change="onInputChange"
      />

      <span
        :class="{dnone: !isInputFieldEmpty && isInputFieldRequired || !isInputFieldRequired}"
      >{{textField.validation_message}}</span>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "TextInput",
  props: {
    textField: {
      type: Object
    }
  },
  data() {
    return {
      inputTextValue: "",
      isInputFieldRequired: this.textField.required,
      isInputFieldEmpty: false
    };
  },
  methods: {
    onInputChange: function() {
      if (this.inputTextValue === "") {
        this.isInputFieldEmpty = true;
      } else {
        this.isInputFieldEmpty = false;
      }
    },
    checkIfRequiredFieldEmpty: function() {
      return this.textField.required && this.inputTextValue === "";
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
          [this.textField.label]: this.inputTextValue
        });
        this.inputTextValue = "";
        this.isInputFieldEmpty = false;
      }
    });
  }
};
</script>