<template>
  <NavbarProject />
  <router-view />
</template>



<script>
import NavbarProject from './components/NavbarProject.vue';
export default {
  components: {
    NavbarProject,
  },
};
</script>



<style>
body {
  margin: 0;
  padding: 0;
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: auto;
  color: #232e3a;
}
</style>
