<template>
  <div id="nav">
    <router-link to="/">Cadastro </router-link>  | 
    <router-link to="/pacientes">Pacientes</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
};
</script>

<style scoped>
#nav {
  background-image: linear-gradient(to right, rgb(194, 47, 88), rgb(194, 17, 67));
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav a {
  color: #222;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
  font-size: 25px;
}

#nav a:hover {
  color: #fff;
}
</style>