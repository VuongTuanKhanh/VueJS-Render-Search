<script>
import EventService from "@/services/EventService.js";
import List from "@/components/List.vue";
import SearchBar from "@/components/SearchBar.vue";
export default {
  render() {
    return (
      <div id="app">
        <SearchBar
          propsFields={this.fields}
          onHandleSubmit={this.handleSubmitRequest}
          onSubmitQuery={this.handleAdvanceRequest}
        />
        <List
          propsItems={this.items}
          propsQueryString={this.queryString}
          propsConditions={this.conditions}
        />
      </div>
    );
  },
  data() {
    return {
      items: [],
      fields: {},
      queryString: "",
      conditions: ""
    };
  },
  created() {
    EventService.getItems()
      .then(respone => {
        this.items = respone.data;
      })
      .catch(error => {
        console.log(error.response);
      });

    EventService.getFields()
      .then(respone => {
        this.fields = respone.data;
      })
      .catch(error => {
        console.log(error.response);
      });
  },
  methods: {
    handleSubmitRequest(queryString) {
      this.queryString = queryString;
    },
    handleAdvanceRequest(queryString, conditions) {
      this.queryString = queryString;
      this.conditions = conditions;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
