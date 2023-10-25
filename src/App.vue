<template>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700;900&family=Pacifico&display=swap"
    rel="stylesheet"
  />

  <div class="container">
    <NavComp></NavComp>
    <router-view></router-view>
  </div>
</template>

<script>
import NavComp from "./components/Naigations.vue";
export default {
  name: "App",
  components: {
    NavComp,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
  outline: none;
}
.container {
  flex-direction: column;

  height: 100vh;
  display: grid;
  grid-template-rows: 1fr 8fr;
}
#app {
  font-family: "Montserrat", sans-serif;
}
</style>
