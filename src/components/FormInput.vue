<template>
  <div>
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
      />

      <span>{{inputField.validation_message}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormInput",
  props: {
    inputField: {
      type: Object
    }
  }
};
</script>

<style lang="scss" scoped>
.form-input {
  width: 40rem;

  input::placeholder {
    font-family: "Fira Sans", sans-serif;
    color: rgb(118, 120, 128);
    font-size: 1.6rem;
  }
}
</style>
