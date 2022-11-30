<template>
  <footer id="footer">
    <p id="content">Pizza Express&copy; 2022</p>
  </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style scoped>
#footer {
  height: 180px;
  background-color: #222;
  border-top: solid #111;
  color: #fcba03;
  display: flex;
  align-items: center;
  justify-content: center;
  bottom: 0;
  width: 100%;
}
#content {
  font-size: large;
}
</style>
