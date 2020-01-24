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
        @change="onEmailChangeHandler"
      />

      <span
        :class="(!inputError && !inputEmailValue || inputEmailValue) ? 'd-none' : null"
      >{{emailField.validation_message}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "EmailInput",
  props: {
    emailField: {
      type: Object
    },
    inputError: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      inputEmailValue: null
    };
  },
  methods: {
    onEmailChangeHandler: function() {
      this.$emit("onEmailChangeHandler", this.inputEmailValue);
    }
  }
};
</script>