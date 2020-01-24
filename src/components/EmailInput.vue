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
        v-model="inputEmail"
        @change="onEmailChangeHandler"
      />

      <span
        :class="(!inputError && !inputEmail || inputEmail) ? 'd-none' : null"
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
      inputEmail: null
    };
  },
  methods: {
    onEmailChangeHandler: function(e) {
      this.$emit("onEmailChangeHandler", e.target.value);
    }
  }
};
</script>