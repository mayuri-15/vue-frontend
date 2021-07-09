<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Get SpringBoot value - {{ backendValue }}</p>
    <button @click="getListOfPeopleFromSpringBoot">Click me</button>
    <button @click="postListOfPeople">Click</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      backendValue: "",
      errors: [],
      peopleList: []
    };
  },
  // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get(
        `http://localhost:8082/api/messages/hello`
      );
      this.backendValue = response.data;
      console.log(this.backendValue);
    } catch (e) {
      this.errors.push(e);
    }
  },
  methods: {
    async getListOfPeopleFromSpringBoot() {
      const response = await axios.get(
        `http://localhost:8082/api/messages/peopleInfo`
      );
      for (var id = 0; id < response.data.length; id++) {
        this.peopleList.push(response.data[id]);
      }
      console.log(this.peopleList);
    },
    async postListOfPeople() {
      let payload = { name: "Akshita", job: "IT" };
      await axios.post("http://localhost:8082/api/messages/sendInfo", payload);
      console.log("posted");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  font: inherit;
  margin-left: 12px;
  border-radius: 12px;
  background-color: brown;
  color: white;
  padding: 0.5rem 2rem;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #5c0556;
  border-color: #5c0556;
}
</style>
