<script>
export default {
  name: "List",
  render() {
    let main_Title = this.titles.map(function(title) {
      return <td>{title}</td>;
    });

    return (
      <table border="1">
        <tr>{main_Title}</tr>
        {this.renderTableData()}
      </table>
    );
  },
  data() {
    return {
      titles: ["Title", "Type", "Owner", "Date", "Star", "Trash"]
    };
  },
  props: {
    items: {
      type: Array
    }
  },
  methods: {
    renderTableData() {
      return this.items.map(item => {
        let rowData = Object.values(item).map(values => {
          return <td>{values}</td>;
        });
        return <tr>{rowData}</tr>;
      });
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
  padding: 15px;
  text-align: center;
}
</style>
