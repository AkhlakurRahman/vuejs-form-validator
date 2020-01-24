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

      <MultiSelect
        :multiSelectInput="multiSelectInput"
        :inputError="inputError"
        @onMultiSelectChangeHandler="onMultiSelectChangeHandler($event)"
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

    <FormDetails
      v-if="showFormTable"
      :inputTextValue="inputTextValue"
      :inputEmailValue="inputEmailValue"
      :multiSelectInputValue="multiSelectInputValue"
      :radioInputValue="radioInputValue"
      :selectInputValue="selectInputValue"
    />
  </div>
</template>

<script>
import TextInput from "./components/TextInput.vue";
import EmailInput from "./components/EmailInput.vue";
import MultiSelect from "./components/MultiSelect.vue";
import SelectInput from "./components/SelectInput.vue";
import RadioInput from "./components/RadioInput.vue";
import FormDetails from "./components/FormDetails.vue";

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
      multiSelectInput: {
        name: "ocupation",
        type: "multiple",
        label: "Ocupation",
        placeholder: "Select Ocupation",
        required: true,
        validation_message: "Ocupation is required",
        options: [
          {
            doctor: "Doctor",
            engineer: "Engineer",
            teacher: "Teacher",
            other: "Other"
          }
        ]
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
      inputTextValue: "",
      inputEmailValue: "",
      multiSelectInputValue: [],
      radioInputValue: "",
      selectInputValue: "",
      inputError: false,
      showFormTable: false
    };
  },
  components: {
    TextInput,
    EmailInput,
    MultiSelect,
    SelectInput,
    RadioInput,
    FormDetails
  },
  methods: {
    onSubmitHandler: function() {
      if (
        this.inputTextValue === "" ||
        this.inputEmailValue === "" ||
        this.radioInputValue === "" ||
        this.selectInputValue === "" ||
        this.multiSelectInputValue.length <= 0
      ) {
        return (this.inputError = true);
      }

      this.showFormTable = true;
    },
    onTextChangeHandler: function(inputTextValue) {
      this.inputTextValue = inputTextValue;
    },
    onEmailChangeHandler: function(inputEmailValue) {
      this.inputEmailValue = inputEmailValue;
    },
    onRadioInputChangeHandler: function(radioInputValue) {
      this.radioInputValue = radioInputValue;
    },
    onSelectChangeHandler: function(selectInputValue) {
      this.selectInputValue = selectInputValue;
    },
    onMultiSelectChangeHandler: function(multiSelectInputValue) {
      this.multiSelectInputValue = [...multiSelectInputValue];
    }
  }
};
</script>

<style lang="scss">
.form-control {
  width: 70vw;
  min-height: 100vh;
  margin: 0 auto;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  h3 {
    font-size: 3rem;
    margin: 3rem 0;
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
    margin-bottom: 3rem;
    transition: all 0.3s ease-in-out;

    &:hover {
      background-color: rgba(100, 255, 218, 0.08);
    }
  }
}
</style>
