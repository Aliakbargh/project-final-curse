<template>
  <div class="project" :class="{ copmalete: project.copmalete }">
    <div class="action">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icon">
        <router-link
          :to="{ name: 'EditProject', params: { id: project.id } }"
        >
          <span @click="editproject" class="material-icons"> edit </span>
        </router-link>
        <span @click="deleteproject" class="material-icons"> delete </span>
        <span @click="doneproject" class="material-icons"> done </span>
      </div>
    </div>
    <div class="details" v-show="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showDetails: false,
      uri: `http://localhost:3000/projects/${this.project.id}`,
    };
  },
  props: ["project"],
  methods: {
    doneproject() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify({ copmalete: !this.project.copmalete }),
      })
        .then(() => this.$emit("copmalete", this.project.id))
        .catch((err) => console.log(err.massage));
    },
    deleteproject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project.id))
        .catch((err) => console.log(err.massage));
    },
    editproject() {},
  },
};
</script>

<style>
.project {
  text-align: center;
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
}
h3 {
  cursor: pointer;
}
.action {
  align-items: center;
  display: flex;
  justify-content: space-between;
}
.material-icons {
  margin-left: 10px;
  cursor: pointer;
  color: #bbb;
  font-size: 24px;
}

.material-icons:hover {
  color: #777;
}
.copmalete {
  background: aquamarine;
}
</style>