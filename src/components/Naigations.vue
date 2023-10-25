<template>
  <div class="container_nav">
    <nav>
      <router-link to="/">Домашняя страница</router-link>
      <router-link to="/chat">Чат</router-link>
      <router-link to="/api">Работа с данными API</router-link>
    </nav>
  </div>
</template>
<script>
export default {
  name: "NavComp",
};
</script>

<style>
.container_nav {
  width: 100%;
  display: flex;
  justify-content: center;
}
nav {
  background: #ffa8b6;
  width: 100%;

  display: flex;
  justify-content: space-around;
  align-items: 30px;
  padding: 30px;
}
a {
  text-decoration: none;
  color: black;
}
</style>
