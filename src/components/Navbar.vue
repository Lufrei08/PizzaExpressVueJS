<template>
  <div id="nav">
    <routerLink to="/" id="logo_url">
      <img :src="logo" :alt="alt" id="logo" />
    </routerLink>
    <router-link to="/">Home</router-link> |
    <router-link to="/pedidos">Pedidos</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
#nav {
  background-color: #222;
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  font-size: larger;
}

#nav #logo_url {
  margin: auto;
  margin-left: 0;
}

#logo {
  width: 70px;
  height: 70px;
}

#nav a {
  color: #fcba03;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
  cursor: pointer;
}

#nav a:hover {
  color: #fff;
}
</style>
