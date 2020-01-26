<template>
  <div>
    <label>
      {{radioInput.label}}
      <sup>&ast;</sup>
    </label>

    <label v-for="(option, index) in radioInput.options[0]" :key="index" class="radio-btn">
      <input
        :name="radioInput.name"
        :type="radioInput.type"
        :value="index"
        v-model="radioInputValue"
        :required="radioInput.required"
        @change="onInputChange"
      />
      {{option}}
      <span class="custom-radio-btn"></span>
    </label>

    <span
      :class="{dnone: !isInputFieldEmpty && isInputFieldRequired || !isInputFieldRequired}"
    >{{radioInput.validation_message}}</span>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "RadioInput",
  props: {
    radioInput: {
      type: Object
    }
  },
  data() {
    return {
      radioInputValue: "",
      isInputFieldRequired: this.radioInput.required,
      isInputFieldEmpty: false
    };
  },
  methods: {
    onInputChange: function() {
      if (this.radioInputValue === "") {
        this.isInputFieldEmpty = true;
      } else {
        this.isInputFieldEmpty = false;
      }
    },

    checkIfRequiredFieldEmpty: function() {
      return this.radioInput.required && this.radioInputValue === "";
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
          [this.radioInput.label]: this.radioInputValue
        });
        this.radioInputValue = "";
        this.isInputFieldEmpty = false;
      }
    });
  }
};
</script>

<style lang="scss" scoped>
.radio-btn {
  color: rgb(136, 146, 176);
  font-size: 1.6rem;
}

.radio-btn input[type="radio"] {
  display: none;
}

.radio-btn {
  position: relative;
  padding-left: 2.5rem;
  display: block;

  .custom-radio-btn {
    display: block;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border: 3px solid rgb(2, 12, 27);
    position: absolute;
    left: 0;
    top: 2px;

    &:after {
      content: "";
      width: 8px;
      height: 8px;
      background-color: rgb(136, 146, 176);
      display: block;
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%) scale(0);
      border-radius: 50%;
      transition: all 0.3s ease-in-out;
    }
  }
}

.radio-btn input[type="radio"]:checked ~ .custom-radio-btn:after {
  transform: translate(-50%, -50%) scale(1);
}
</style>