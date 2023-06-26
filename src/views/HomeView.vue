<template>
  <div class="home">
    <FilterProject @updateProject="current = $event" :current="current" />
    <div v-for="project in sortProject" :key="project.id">
      <SingleProject
        :project="project"
        @deleteProject="handleProject"
        @updateComplate="handleComplate" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SingleProject from "@/components/SingleProject.vue";
import FilterProject from "@/components/FilterProject.vue";

// @ is an alias to /src

export default {
  name: "HomeView",
  components: { SingleProject, FilterProject },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  async mounted() {
    let response = await axios.get("http://localhost:3000/projects");
    this.projects = response.data;
  },
  methods: {
    handleProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplate(id) {
      let findProject = this.projects.find((project) => project.id == id);
      findProject.complated = !findProject.complated;
    },
  },
  computed: {
    sortProject() {
      if (this.current === "all") {
        return this.projects;
      }
      if (this.current === "complate") {
        return this.projects.filter((project) => project.complated == true);
      }
      if (this.current === "process") {
        return this.projects.filter((project) => project.complated == false);
      }
    },
  },
};
</script>
