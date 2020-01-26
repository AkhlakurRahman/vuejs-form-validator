<template>
  <div class="form-details">
    <table>
      <tr>
        <th v-for="(d, index) in data[0]" :key="index">{{index}}</th>
      </tr>
      <tr v-for="(ata, index) in data" :key="index">
        <td v-for="(value, i) in ata" :key="i">{{capitalizedFirstLetter(value)}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "FormDetails",
  props: {
    data: {
      type: Array
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