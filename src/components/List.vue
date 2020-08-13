<script>
export default {
  name: "List",
  render() {
    let main_Title = this.titles.map(function(title) {
      return (
        <td>
          <b>{title}</b>
        </td>
      );
    });

    return (
      <table border="1">
        <tr>{main_Title}</tr>
        {this.renderTableData}
      </table>
    );
  },
  data() {
    return {
      titles: ["Title", "Type", "Owner", "Date", "Star", "Trash"],
      showList: this.items
    };
  },
  props: {
    items: {
      type: Array
    },
    queryString: {
      type: String
    }
  },
  watch: {
    items() {
      this.showList = this.items;
    },
    queryString() {
      console.log("List:", this.queryString);
      let filteredList = [];
      for (let item of this.items) {
        let itemQueryString = "";
        Object.entries(item).map(
          ([key, value]) => (itemQueryString += key + ":" + value + " ")
        );
        let isFalse = false;
        for (let condition of this.queryString.split(" ")) {
          if (!itemQueryString.includes(condition)) {
            isFalse = true;
            break;
          }
        }
        if (!isFalse) {
          filteredList.push(item);
        }
      }
      this.showList = filteredList;
    }
  },
  computed: {
    renderTableData() {
      return this.showList.map(item => {
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
