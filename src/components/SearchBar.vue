<script>
export default {
  name: "SearchBar",
  render() {
    return (
      <div class="container">
        <div class="search-container">
          <input
            type="text"
            placeholder="Search..."
            class="search-bar"
            id="searchBar"
            onClick={() => this.openForm("myForm")}
          />
          <button class="close-button">X</button>
        </div>
        <div class="form-popup" id="myForm">
          <div class="form-container">
            <button class="btn" onClick={() => this.createQuery("Site")}>
              Sites
            </button>
            <button class="btn" onClick={() => this.createQuery("Page")}>
              Pages
            </button>
            <button class="btn" onClick={() => this.createQuery("Advance")}>
              Advance Search
            </button>
          </div>
        </div>
      </div>
    );
  },
  methods: {
    openForm(id) {
      document.getElementById(id).style.display = "block";
    },
    closeForm(id) {
      document.getElementById(id).style.display = "none";
    },
    createQuery(type) {
      this.closeForm("myForm");
      let queryString = "";
      if (type == "Site") {
        queryString = "Type:Site";
      } else if (type == "Page") {
        queryString = "Type:Page";
      }
      document.getElementById("searchBar").value = queryString;
      this.$emit("handleSubmit", queryString);
    }
  }
};
</script>
<style scoped>
.container {
  width: 100%;
  margin-bottom: 20px;
}
.form-popup {
  display: none;
  position: fixed;
  width: 100%;
  z-index: 9;
}
.form-container .btn:hover {
  opacity: 1;
}
.form-container .btn {
  font-weight: bolder;
  font-size: 20px;
  text-align: left;
  padding: 16px 20px;
  border: none;
  cursor: pointer;
  max-width: 98%;
  width: 100%;
  margin: 10px 20px 0px 10px;
  opacity: 0.8;
}
.form-container {
  width: 50%;
  margin: auto;
  background-color: white;
}
.search-container {
  display: flex;
  width: 50%;
  margin: auto;
  margin-top: 20px;
}
.search-bar {
  padding: 10px;
  position: relative;
  font-size: 17px;
  border: 1px solid grey;
  float: left;
  width: 80%;
  background: #f1f1f1;
}
.close-button {
  float: left;
  width: 20%;
  padding: 10px;
  background: #2196f3;
  color: white;
  font-size: 17px;
  border: 1px solid grey;
  border-left: none;
  cursor: pointer;
}
</style>
