<template>
  <div class="form-input">
    <label :for="inputField.name">
      {{inputField.label}}
      <sup>&ast;</sup>
    </label>

    <input
      :type="inputField.type"
      :placeholder="inputField.placeholder"
      :name="inputField.name"
      :id="inputField.name"
      v-model.lazy="userData[inputField.name]"
    />

    <span
      :class="{dnone: !isInputFieldEmpty && isInputFieldRequired}"
    >{{inputField.validation_message}}</span>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "CommonInput",
  props: {
    inputField: {
      type: Object
    }
  },
  data() {
    return {
      userData: {
        [this.inputField.name]: ""
      },
      isInputFieldRequired: this.inputField.required,
      isInputFieldEmpty: false
    };
  },
  methods: {
    checkIfInputFieldEmpty: function() {
      if (this.userData[this.inputField.name] === "") {
        return (this.isInputFieldEmpty = true);
      }
      this.isInputFieldEmpty = false;
    },
    checkIfRequiredFiledEmpty: function() {
      const { name, required } = this.inputField;
      return required && this.userData[name] === "";
    }
    //   Object.keys(this.inputField).forEach(key => {
    //     if (key === "name") {
    //       if (this.userData[name] === "") {
    //         return (this.isInputFieldEmpty = true);
    //       }
    //       this.isInputFieldEmpty = false;
    //     }
    //   });
    // }
    // checkIfRequiredFiledEmpty: function() {
    //   Object.keys(this.inputField).forEach(key => {
    //     if (key === "name" && key === "required") {
    //       return required && this.userData[name] === "";
    //     }
    //   });
    // }
  },
  created() {
    eventBus.$on("onSubmitHandler", () => {
      this.checkIfInputFieldEmpty();

      if (!this.isInputFieldEmpty) {
        const { name } = this.inputField;
        eventBus.$emit("onSuccesSubmission", {
          [name]: this.userData[name],
          [name]: this.userData[name]
        });
        this.userData[name] = "";
      }
    });
  }
};
</script>

<style lang="scss" scoped>
</style>