<template>
  <div class="form-control">
    <form @submit.prevent="onSubmitHandler">
      <div v-for="(formField, index) in formFields.fields" :key="index">
        <div v-html="formField.content"></div>
        <TextInput
          v-if="formField.type=== 'text'"
          :textField="formField"
          :inputError="inputError"
          @onTextChangeHandler="onTextChangeHandler($event)"
        />

        <EmailInput
          v-if="formField.type=== 'email'"
          :emailField="formField"
          :inputError="inputError"
          @onEmailChangeHandler="onEmailChangeHandler($event)"
        />

        <MultiSelect
          v-if="formField.type=== 'multi-select'"
          :multiSelectInput="formField"
          :inputError="inputError"
          @onMultiSelectChangeHandler="onMultiSelectChangeHandler($event)"
        />

        <RadioInput
          v-if="formField.type=== 'radio'"
          :radioInput="formField"
          :inputError="inputError"
          @onRadioInputChangeHandler="onRadioInputChangeHandler($event)"
        />

        <SelectInput
          v-if="formField.type=== 'select'"
          :singleSelect="formField"
          :inputError="inputError"
          @onSelectChangeHandler="onSelectChangeHandler($event)"
        />
      </div>
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
import formFields from "./utils/formFields";
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
      formFields,
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
