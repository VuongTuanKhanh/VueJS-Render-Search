<template>
  <div>
    <table border="1">
      <tr>
        <td></td>
        <td><h3>Title</h3></td>
        <td><h3>Type</h3></td>
        <td><h3>Owner</h3></td>
        <td><h3>Date</h3></td>
        <td><h3>Starred</h3></td>
        <td><h3>Trash</h3></td>
      </tr>
      <tr v-for="(item, index) in items" :key="item.Title">
        <td>{{ index }}</td>
        <td>{{ item.Title }}</td>
        <td>{{ item.Type }}</td>
        <td>{{ item.Owner }}</td>
        <td>{{ item.Date }}</td>
        <td>{{ item.Starred }}</td>
        <td>{{ item.Trash }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "List",
  props: {
    items: {
      type: Array
    }
  }
};
</script>

<style scoped>
table {
  width: 90%;
  margin: auto;
}

tr {
  width: 80%;
}

td {
  width: 200px;
  text-align: center;
}
</style>
