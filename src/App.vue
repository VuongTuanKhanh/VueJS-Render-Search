<script>
import EventService from "@/services/EventService.js";
import List from "@/components/List.vue";
export default {
  components: {
    List
  },
  render(h) {
    return h(List, {
      class: {
        list: true
      },
      props: {
        items: this.items,
        query: this.query
      }
    });
  },
  data() {
    return {
      items: []
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
  methods: {}
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
