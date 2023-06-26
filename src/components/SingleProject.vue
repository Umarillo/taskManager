<template>
  <div class="project" :class="{ activeComplate: project.complated }">
    <div class="actions">
      <h3 @click="showDeadline = !showDeadline">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons" @click="compladeMethod">done</span>
        <span class="material-icons" @click="deleteProject">delete</span>
        <router-link :to="{ name: 'editProject', params: { id: project.id } }">
          <span class="material-icons">edit</span></router-link
        >
      </div>
    </div>
    <div class="deadline" v-if="showDeadline">
      <p>{{ project.deadline }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["project"],
  data() {
    return {
      showDeadline: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    async deleteProject() {
      await axios.delete(this.url);
      this.$emit("deleteProject", this.project.id);
    },
    async compladeMethod() {
      await axios.patch(this.url, {
        complated: !this.project.complated,
      });
      this.$emit("updateComplate", this.project.id);
    },
  },
};
</script>

<style scoped>
.project {
  margin: 20px;
  background: #fff;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 05);
  border-left: 15px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
.activeComplate {
  border-left: 15px solid green;
}
</style>
