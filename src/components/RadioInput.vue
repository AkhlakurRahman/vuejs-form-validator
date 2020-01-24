<template>
  <div>
    <label>
      <slot />
      <sup>&ast;</sup>
    </label>

    <label v-for="(option, index) in options[0]" :key="index" class="radio-btn">
      <input :value="index" v-bind="$attrs" />
      {{option}}
      <span class="custom-radio-btn"></span>
    </label>
    <slot name="validation_message" />
  </div>
</template>

<script>
export default {
  name: "RadioInput",
  props: {
    options: {
      type: Array
    }
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