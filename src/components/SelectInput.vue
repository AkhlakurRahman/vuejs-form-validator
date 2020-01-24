<template>
  <div class="select-input">
    <label :for="singleSelect.name">
      {{singleSelect.label}}
      <sup>&ast;</sup>
    </label>
    <select :name="singleSelect.name" :id="singleSelect.name">
      <option value="default">Select a status</option>
      <option
        v-for="(option, index) in singleSelect.options[0]"
        :value="index"
        :key="index"
      >{{ option }}</option>
    </select>

    <span>{{singleSelect.validation_message}}</span>
  </div>
</template>

<script>
export default {
  name: "SelectInput",
  props: {
    singleSelect: {
      type: Object
    }
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
