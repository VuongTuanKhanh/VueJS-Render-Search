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
        let { Title, Type, Owner, Date, Starred, Trash } = item;
        return (
          <tr>
            <td>{Title}</td>
            <td>{Type}</td>
            <td>{Owner}</td>
            <td>{Date}</td>
            <td>{Starred}</td>
            <td>{Trash}</td>
          </tr>
        );
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
