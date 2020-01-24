<template>
  <div class="form-control">
    <h3>Please fill up the following form</h3>
    <form @submit.prevent="onSubmit">
      <FormInput
        focusAttribute="first_name"
        type="text"
        placeholder="First Name"
        required="true"
      >First Name</FormInput>
      <span slot="validation_message">First name is required</span>

      <FormInput focusAttribute="email" type="email" placeholder="Email" required="true">Email</FormInput>
      <span slot="validation_message">Email is required</span>

      <RadioInput type="radio" :options="options" name="status">Status</RadioInput>
      <span slot="validation_message">Status is required</span>

      <SelectInput name="internal_status" :options="options">Internal Status</SelectInput>
      <span slot="validation_message">Internal Status is required</span>

      <button type="submit" class="btn">Submit</button>
    </form>
  </div>
</template>

<script>
import FormInput from "./components/FormInput.vue";
import SelectInput from "./components/SelectInput.vue";
import RadioInput from "./components/RadioInput.vue";

export default {
  name: "app",
  data() {
    return {
      options: [
        {
          valid: "Valid",
          invalid: "Invalid"
        }
      ]
    };
  },
  components: {
    FormInput,
    SelectInput,
    RadioInput
  },
  methods: {
    onSubmit: () => {
      console.log("Submitted");
    }
  }
};
</script>

<style lang="scss">
.form-control {
  width: 60vw;
  height: 100vh;
  margin: 0 auto;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  h3 {
    font-size: 2.5rem;
    margin-bottom: 2rem;
  }

  label {
    display: block;
    font-size: 2rem;
    margin-bottom: 0.7rem;
  }

  span {
    display: block;
    color: rgb(153, 49, 49);
    font-size: 1.2rem;
    margin-bottom: 1.5rem;
  }

  sup {
    color: rgb(153, 49, 49);
  }

  .btn {
    cursor: pointer;
    font-family: "Fira Sans", sans-serif;
    font-size: 1.8rem;
    color: rgb(100, 255, 218);
    background-color: rgb(10, 25, 47);
    border: 1px solid rgb(100, 255, 218);
    border-radius: 3px;
    padding: 1.25rem 3.5rem;
    margin-top: 3rem;
    transition: all 0.3s ease-in-out;

    &:hover {
      background-color: rgba(100, 255, 218, 0.08);
    }
  }
}
</style>
