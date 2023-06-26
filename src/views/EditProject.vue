<template>
  <form @submit.prevent="handeleEditProject">
    <label> Title:</label>
    <input type="text" v-model="title" />
    <label> Deadline:</label>
    <textarea required v-model="deadline"></textarea>
    <button>Add New Project</button>
  </form>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      deadline: "",
    };
  },
  async mounted() {
    let { data } = await axios.get("http://localhost:3000/projects/" + this.id);
    this.title = data.title; 
    this.deadline = data.deadline;
  },
  methods: {
    async handeleEditProject() {
      await axios.patch(`http://localhost:3000/projects/${this.id}`, {
        title: this.title,
        deadline: this.deadline,
      });
      this.$router.push({ name: "home" });
    },
  },
};
</script>

<style scoped>
form {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: white;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  border: 1px solid#ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}
form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
