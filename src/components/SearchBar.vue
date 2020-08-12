<script>
export default {
  name: "SearchBar",
  render() {
    return (
      <div>
        <input type="text" placeholder="Search.." />
        <button>X</button>
      </div>
    );
  },
  methods: {
    handleMouseOver() {
      console.log("click");
    }
  }
};
</script>
<style scoped>
div {
  display: flex;
  width: 50%;
  margin: auto;
  margin-bottom: 20px;
  margin-top: 20px;
}
input {
  padding: 10px;
  font-size: 17px;
  border: 1px solid grey;
  float: left;
  width: 80%;
  background: #f1f1f1;
}
button {
  float: left;
  width: 15%;
  padding: 10px;
  background: #2196f3;
  color: white;
  font-size: 17px;
  border: 1px solid grey;
  border-left: none;
  cursor: pointer;
}
</style>
