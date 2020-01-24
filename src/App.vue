<template>
  <div class="form-control">
    <h3>Please fill up the following form</h3>
    <form @submit.prevent="onSubmitHandler">
      <TextInput
        :textField="firstName"
        :inputError="inputError"
        @onTextChangeHandler="onTextChangeHandler($event)"
      />

      <EmailInput
        :emailField="email"
        :inputError="inputError"
        @onEmailChangeHandler="onEmailChangeHandler($event)"
      />

      <RadioInput
        :radioInput="radioInput"
        :inputError="inputError"
        @onRadioInputChangeHandler="onRadioInputChangeHandler($event)"
      />

      <SelectInput
        :singleSelect="singleSelect"
        :inputError="inputError"
        @onSelectChangeHandler="onSelectChangeHandler($event)"
      />

      <button type="submit" class="btn">Submit</button>
    </form>
  </div>
</template>

<script>
import TextInput from "./components/TextInput.vue";
import EmailInput from "./components/EmailInput.vue";
import SelectInput from "./components/SelectInput.vue";
import RadioInput from "./components/RadioInput.vue";

export default {
  name: "app",
  data() {
    return {
      firstName: {
        name: "first_name",
        type: "text",
        label: "First Name",
        placeholder: "First Name",
        required: true,
        validation_message: "First name is required"
      },
      email: {
        name: "email",
        label: "Email",
        type: "email",
        placeholder: "Email",
        required: true,
        validation_message: "Email is required"
      },
      singleSelect: {
        name: "internal_status",
        type: "select",
        label: "Internal Status",
        required: true,
        validation_message: "Internal Status is required",
        options: [
          {
            valid: "Valid",
            invalid: "Invalid"
          }
        ]
      },
      radioInput: {
        name: "status",
        type: "radio",
        label: "Status",
        required: true,
        validation_message: "Status is required",
        options: [
          {
            valid: "Valid",
            invalid: "Invalid"
          }
        ]
      },
      textInput: "",
      emailInput: "",
      radioBtnInput: "",
      selectInput: "",
      inputError: false
    };
  },
  components: {
    TextInput,
    EmailInput,
    SelectInput,
    RadioInput
  },
  methods: {
    onSubmitHandler: function() {
      if (
        this.textInput === "" ||
        this.emailInput === "" ||
        this.radioBtnInput === "" ||
        this.selectInput === ""
      ) {
        return (this.inputError = true);
      }

      console.log("Submitted");
    },
    onTextChangeHandler: function(textInput) {
      this.textInput = textInput;
    },
    onEmailChangeHandler: function(emailInput) {
      this.emailInput = emailInput;
    },
    onRadioInputChangeHandler: function(radioInput) {
      this.radioBtnInput = radioInput;
    },
    onSelectChangeHandler: function(selectInput) {
      this.selectInput = selectInput;
    }
  }
};
</script>

<style lang="scss">
.form-control {
  width: 60vw;
  min-height: 100vh;
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
    margin-bottom: 0rem;
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
