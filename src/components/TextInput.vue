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
        v-model="inputText"
        @change="onTextChangeHandler"
      />

      <span
        :class="(!inputError && !inputText || inputText) ? 'd-none' : null"
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
      inputText: null
    };
  },
  methods: {
    onTextChangeHandler: function(e) {
      this.$emit("onTextChangeHandler", e.target.value);
    }
  }
};
</script>