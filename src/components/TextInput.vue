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
        @change="onTextChangeHandler"
      />

      <span
        :class="(!inputError && !inputTextValue || inputTextValue) ? 'd-none' : null"
      >{{textField.validation_message}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TextInput",
  props: {
    textField: {
      type: Object
    },
    inputError: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      inputTextValue: null
    };
  },
  methods: {
    onTextChangeHandler: function() {
      this.$emit("onTextChangeHandler", this.inputTextValue);
    }
  }
};
</script>