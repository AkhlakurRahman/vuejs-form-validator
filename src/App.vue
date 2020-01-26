<template>
  <div class="form-control">
    <form>
      <div v-for="(formField, index) in formFields.fields" :key="index">
        <div v-html="formField.content"></div>

        <TextInput v-if="formField.type=== 'text'" :textField="formField" />

        <EmailInput v-if="formField.type === 'email'" :emailField="formField" />

        <MultiSelect v-if="formField.type=== 'multi-select'" :multiSelectInput="formField" />

        <RadioInput v-if="formField.type=== 'radio'" :radioInput="formField" />

        <SelectInput v-if="formField.type=== 'select'" :singleSelect="formField" />
      </div>
      <button type="submit" @click.prevent="onSubmitHandler" class="btn">Submit</button>
    </form>

    <FormDetails v-if="showDataTable > 0" :data="allFormData" />
    {{allFormData}}
  </div>
</template>

<script>
import formFields from "./utils/formFields";
import TextInput from "./components/TextInput.vue";
import EmailInput from "./components/EmailInput.vue";
import MultiSelect from "./components/MultiSelect.vue";
import SelectInput from "./components/SelectInput.vue";
import RadioInput from "./components/RadioInput.vue";
import FormDetails from "./components/FormDetails";
import { eventBus } from "./main";

export default {
  name: "app",
  data() {
    return {
      formFields,
      individualData: {},
      formData: [],
      // passedAllValidation: false,
      showDataTable: false
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
      if (!this.passedAllValidation) {
        eventBus.$emit("onSubmitHandler");
      }
    }

    // allFormData: function() {
    //   this.formData.push({
    //     formField: { ...this.individualData }
    //   });
    // }
  },
  computed: {
    allFormData: function() {
      const data = [];
      data.push({
        ...this.individualData
      });
      return data;
    }
  },
  created() {
    eventBus.$on("passedAllValidation", data => {
      this.passedAllValidation = data;
    });

    eventBus.$on("onSuccesSubmission", data => {
      this.individualData = { ...this.individualData, ...data };
      this.showDataTable = true;
    });
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
