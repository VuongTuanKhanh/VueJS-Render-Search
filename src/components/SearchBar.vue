<script>
export default {
  name: "SearchBar",
  render() {
    return (
      <div class="container">
        <div class="search-container">
          <input
            type="text"
            placeholder="Search.."
            class="search-bar"
            onClick={this.openForm}
          />
          <button class="close-button">X</button>
        </div>
        <div class="form-popup" id="myForm">
          <div class="form-container">{this.search_Type_List()}</div>
        </div>
      </div>
    );
  },
  methods: {
    openForm() {
      document.getElementById("myForm").style.display = "block";
    },
    closeForm() {
      document.getElementById("myForm").style.display = "none";
    },
    createQuery() {
      console.log("type");
    },
    search_Type_List() {
      return this.search_Types.map(function(type) {
        return (
          <button class="btn" onClick="createQuery()">
            {type}
          </button>
        );
      });
    }
  },
  data() {
    return {
      search_Types: ["Sites", "Pages", "Advance Search"]
    };
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
