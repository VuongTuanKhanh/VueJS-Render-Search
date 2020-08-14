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
      showList: this.items,
      startDate: "",
      endDate: "",
      isNotme: ""
    };
  },
  props: {
    items: {
      type: Array
    },
    queryString: {
      type: String
    },
    conditions: {
      type: String
    }
  },
  methods: {
    filtering() {
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
      if (this.isNotme == "true") {
        for (let i in this.showList) {
          if (this.showList[i].Owner == "Khanh") {
            delete this.showList[i];
          }
        }
      }
    }
  },
  watch: {
    items() {
      this.showList = this.items;
    },
    conditions() {
      let conditions = this.conditions.split("&");
      this.startDate = conditions[0];
      this.endDate = conditions[1];
      this.isNotme = conditions[2];
      this.filtering();
    },
    queryString() {
      this.filtering();
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
