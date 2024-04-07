<template>
  <FilterNavbar @changeFilter="current = $event" :current="current" />
  <!-- handler => handler(by)-->
  <div class="home">
    <div v-if="dataProjects.length">
      <div v-for="project in filterProject" :key="project.id">
        <SingelProjectVue
          :project="project"
          @delete="handelDelete"
          @copmalete="handelCopmalete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingelProjectVue from "../components/SingelProject.vue";
import FilterNavbar from "../components/FilterNavbar.vue";

export default {
  name: "HomeView",
  components: { SingelProjectVue, FilterNavbar },
  data() {
    return {
      current: "all",
      dataProjects: [],
    };
  },
  methods: {
    handelDelete(deleteProjectId) {
      this.dataProjects = this.dataProjects.filter((item) => {
        return item.id !== deleteProjectId;
      });
    },
    handelCopmalete(deleteProjectId) {
      let proj = this.dataProjects.find((item) => {
        return item.id === deleteProjectId;
      });
      proj.copmalete = !proj.copmalete;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.dataProjects = data))
      .catch((err) => console.log(err.massage));
  },
  computed: {
    filterProject() {
      if (this.current === "copmalete") {
        return this.dataProjects.filter((item) => item.copmalete);
      } else if (this.current === "Ongoing") {
        return this.dataProjects.filter((item) => !item.copmalete);
      }else{
        return this.dataProjects
      }
    },
  },
};
</script>
