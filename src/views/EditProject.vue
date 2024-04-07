<template>
  <form @submit.prevent="handelSubmit">
    <label>Title: </label>
    <input type="text" required v-model="title" />
    <label>Details:</label>
    <textarea v-model="details"></textarea>
    <button>Updata Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      uri: `http://localhost:3000/projects/${this.id}`,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      })
      .catch((err) => console.log(err.massage));
  },
  methods: {
    handelSubmit() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify({
            title: this.title,
            details: this.details,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.massage));
      this.details = "";
      this.title = "";
    },
  },
};
</script>

<style>
form {
  background: white;
  padding: 20px;
  border-radius: 15px;
}
label {
  display: block;
  color: #bbb;
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
  border: 2px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100%;
}
form button {
  display: block;
  padding: 10px;
  border: 0;
  color: #00ce89;
  margin: 20px auto 0;
  box-sizing: border-box;
  border-radius: 6px;
  font-size: 16px;
}
</style>