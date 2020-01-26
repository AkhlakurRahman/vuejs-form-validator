<template>
  <div>
    <div class="form-input">
      <label :for="emailField.name">
        {{emailField.label}}
        <sup>&ast;</sup>
      </label>

      <input
        :type="emailField.type"
        :placeholder="emailField.placeholder"
        :name="emailField.name"
        :id="emailField.name"
        v-model="inputEmailValue"
        :required="emailField.required"
        @change="onInputChange"
      />

      <span
        :class="{dnone: !isInputFieldEmpty && isInputFieldRequired || !isInputFieldRequired}"
      >{{emailField.validation_message}}</span>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "EmailInput",
  props: {
    emailField: {
      type: Object
    }
  },
  data() {
    return {
      inputEmailValue: "",
      isInputFieldRequired: this.emailField.required,
      isInputFieldEmpty: false
    };
  },
  methods: {
    onInputChange: function() {
      if (this.inputEmailValue === "") {
        this.isInputFieldEmpty = true;
      } else {
        this.isInputFieldEmpty = false;
      }
    },

    checkIfRequiredFieldEmpty: function() {
      return this.emailField.required && this.inputEmailValue === "";
    }
  },
  created() {
    eventBus.$on("onSubmitHandler", () => {
      this.onInputChange();

      if (!this.isInputFieldEmpty && !this.checkIfRequiredFieldEmpty()) {
        eventBus.$emit("onSuccesSubmission", {
          [this.emailField.label]: this.inputEmailValue
        });
        this.inputEmailValue = "";
        this.isInputFieldEmpty = false;
      }
    });
  }
};
</script>