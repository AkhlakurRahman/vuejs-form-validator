<template>
  <div class="form-details">
    <table>
      <tr>
        <th>First Name</th>
        <th>Email</th>
        <th>Occupations</th>
        <th>Status</th>
        <th>Internal Status</th>
      </tr>
      <tr>
        <td>{{inputTextValue}}</td>
        <td>{{inputEmailValue}}</td>
        <td>{{capitalizedFirstLetter(multiSelectInputValue)}}</td>
        <td>{{capitalizedFirstLetter(radioInputValue)}}</td>
        <td>{{capitalizedFirstLetter(selectInputValue)}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "FormDetails",
  props: {
    inputTextValue: {
      type: String
    },
    inputEmailValue: {
      type: String
    },
    multiSelectInputValue: {
      type: Array
    },
    radioInputValue: {
      type: String
    },
    selectInputValue: {
      type: String
    }
  },
  methods: {
    capitalizedFirstLetter: function(selectArray) {
      if (typeof selectArray === "string") {
        return selectArray.charAt(0).toUpperCase() + selectArray.slice(1);
      }

      const items = selectArray.map(item => {
        return item.charAt(0).toUpperCase() + item.slice(1);
      });

      return items.join(", ");
    }
  }
};
</script>

<style lang="scss" scoped>
.form-details {
  margin-bottom: 4rem;

  table {
    border-collapse: collapse;
    font-size: 1.8rem;
    width: 100%;

    td,
    th {
      border: 1px solid #dddddd;
      text-align: left;
      padding: 8px;
    }
  }
}
</style>