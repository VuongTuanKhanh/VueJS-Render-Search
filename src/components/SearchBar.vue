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
            readonly
            domPropsValue={this.queryString}
            onClick={() => this.openForm("myForm")}
          />
          <button class="close-button" onClick={this.closeAllForm}>
            X
          </button>
        </div>
        <div class="form-popup" id="myForm">
          <div class="form-container">
            <button class="btn" onClick={() => this.createQuery("Site")}>
              Sites
            </button>
            <button class="btn" onClick={() => this.createQuery("Page")}>
              Pages
            </button>
            <button
              class="btn"
              onClick={() => this.closeForm("myForm", "advanceForm")}
            >
              Advance Search
            </button>
          </div>
        </div>
        <div class="form-popup" id="advanceForm">
          <div class="form-container">
            {this.Types()}
            {this.Owners()}
            {this.SpecificName()}
            {this.Status()}
            {this.Dates()}
            {this.SelectDate()}
            {this.SearchTerm()}
            <button class="btn-search" onClick={this.handleSubmit}>
              Search
            </button>
          </div>
        </div>
      </div>
    );
  },
  props: {
    fields: {
      type: Object
    }
  },
  data() {
    return {
      type: "",
      owner: "",
      name: "",
      isNotme: false,
      starred: "",
      trash: "",
      date: "",
      startDate: "",
      endDate: "",
      term: ""
    };
  },
  methods: {
    openForm(openid, closeid = "") {
      document.getElementById(openid).style.display = "block";
      if (closeid) {
        document.getElementById(closeid).style.display = "none";
      }
    },
    closeForm(closeid, openid = "") {
      document.getElementById(closeid).style.display = "none";
      if (openid) {
        document.getElementById(openid).style.display = "block";
      }
    },
    closeAllForm() {
      this.closeForm("myForm");
      this.closeForm("advanceForm");
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
    },
    Types() {
      let options = this.fields.Advance.map(type => {
        return <option>{type}</option>;
      });
      return (
        <div>
          <label>Type</label>
          <select onChange={$event => this.changeType($event)}>
            {options}
          </select>
        </div>
      );
    },
    Owners() {
      let options = this.fields.Owners.map(type => {
        return <option>{type}</option>;
      });
      return (
        <div>
          <label>Own</label>
          <select onChange={$event => this.changeOwner($event)}>
            {options}
          </select>
        </div>
      );
    },
    SpecificName() {
      return (
        <div>
          <input
            type="text"
            class="input-box"
            id="SpecificPerson"
            domPropsValue={this.owner}
            onKeyup={$event => this.handleInput($event)}
          />
        </div>
      );
    },
    Dates() {
      let options = this.fields.Date.map(type => {
        return <option>{type}</option>;
      });
      return (
        <div>
          <label>Date</label>
          <select onChange={$event => this.changeDate($event)}>
            {options}
          </select>
        </div>
      );
    },
    SelectDate() {
      return (
        <div>
          <input
            type="date"
            class="date-range"
            onChange={$event => this.changeStartDate($event)}
          />
          <input
            type="date"
            class="date-range"
            onChange={$event => this.changeEndDate($event)}
          />
        </div>
      );
    },
    changeStartDate(e) {
      this.startDate = e.target.value;
    },
    changeEndDate(e) {
      this.endDate = e.target.value;
    },
    Status() {
      let fieldName = this.fields.Status.map(type => {
        return (
          <span>
            <input type="checkbox" id={type} onChange={this.changeStatus} />
            <span>{type}</span>
          </span>
        );
      });
      return <div>{fieldName}</div>;
    },
    changeStatus() {
      this.starred =
        "Starred:" + document.getElementById("Starred").checked + " ";
      this.trash = "Trash:" + document.getElementById("Trash").checked + " ";
    },
    changeDate(e) {
      let value = e.target.value;
      for (let i of document.getElementsByClassName("date-range")) {
        i.style.display = "none";
      }
      if (value == "Anytime") {
        this.startDate = "";
        this.endDate = "";
        this.date = "";
      } else if (value == "Today") {
        this.date =
          "Date:" +
          new Date()
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-") +
          " ";
      } else if (value == "Yesterday") {
        this.date =
          "Date:" +
          new Date(new Date().setDate(new Date().getDate() - 1))
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-") +
          " ";
      } else {
        this.date = "";
        if (value == "Last 7 days") {
          this.startDate = new Date(
            new Date().setDate(new Date().getDate() - 7)
          )
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-");
          this.endDate = new Date()
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-");
        } else if (value == "Last 30 days") {
          this.startDate = new Date(
            new Date().setDate(new Date().getDate() - 30)
          )
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-");
          this.endDate = new Date()
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-");
        } else if (value == "Last 90 days") {
          this.startDate = new Date(
            new Date().setDate(new Date().getDate() - 90)
          )
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-");
          this.endDate = new Date()
            .toJSON()
            .slice(0, 10)
            .replace(/-/g, "-");
        } else if (value == "Custom...") {
          for (let i of document.getElementsByClassName("date-range")) {
            i.style.display = "inline-block";
          }
        }
      }
    },
    changeTerm(e) {
      this.term = e.target.value;
    },
    SearchTerm() {
      return (
        <div>
          <label>Term</label>
          <input
            type="text"
            id="search-term"
            onChange={$event => this.changeTerm($event)}
          />
        </div>
      );
    },
    handleInput(e) {
      if (event.keyCode == 13) {
        this.owner = "Owner:" + e.target.value + " ";
        document.getElementById("SpecificPerson").style.display = "none";
      }
    },
    changeType(e) {
      let value = e.target.value;
      if (value != "All types") {
        this.type = "Type:" + value + " ";
      } else {
        this.type = "";
      }
    },
    changeOwner(e) {
      this.isNotme = false;
      let value = e.target.value;
      if (value == "Specific Person...") {
        this.owner = "";
        document.getElementById("SpecificPerson").style.display = "block";
      } else {
        document.getElementById("SpecificPerson").style.display = "none";
        this.owner = value;
        if (this.owner == "Owned by me") {
          this.owner = "Owner:Khanh ";
        } else if (this.owner == "Not owned by me") {
          this.owner = "";
          this.isNotme = true;
        } else {
          this.owner = "";
        }
      }
    },
    handleSubmit() {
      this.$emit("submitQuery", this.queryString, this.conditions);
      this.closeAllForm();
    }
  },
  computed: {
    queryString() {
      return (
        this.type +
        this.owner +
        this.name +
        this.starred +
        this.trash +
        this.date +
        this.term
      );
    },
    conditions() {
      return this.startDate + "&" + this.endDate + "&" + this.isNotme;
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
.date-range {
  position: relative;
  cursor: pointer;
  width: 35%;
  font-size: 18px;
  margin: auto;
  margin-bottom: 10px;
  margin-top: 15px;
  margin-left: 10px;
  opacity: 0.8;
  display: none;
}
.form-container .btn:hover {
  opacity: 1;
}
.btn-search {
  font-weight: bolder;
  font-size: 20px;
  text-align: center;
  padding: 16px 20px;
  border: none;
  cursor: pointer;
  max-width: 20%;
  width: 20%;
  margin: 10px 20px 20px 10px;
  background-color: #2196f3;
  opacity: 0.8;
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
span {
  font-size: 20px;
  padding: 10px;
}
select {
  padding: 16px 20px;
  position: relative;
  cursor: pointer;
  max-width: 86%;
  width: 86%;
  font-size: 20px;
  margin: 10px 0px 0px 10px;
  opacity: 0.8;
}
#search-term {
  padding: 16px 20px;
  position: relative;
  cursor: pointer;
  max-width: 79.5%;
  width: 80%;
  font-size: 18px;
  margin: 10px 0px 0px 10px;
  opacity: 0.8;
}
.input-box {
  padding: 16px 20px;
  position: relative;
  cursor: pointer;
  width: 50%;
  font-size: 18px;
  margin: auto;
  margin-bottom: 10px;
  margin-top: 10px;
  opacity: 0.8;
  display: none;
}
option {
  font-size: 20px;
}
label {
  font-weight: bolder;
  font-size: 20px;
  position: relative;
  text-align: left;
  border: none;
  max-width: 10%;
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
