<template>
  <Banner />
  <div class="main-container">
    <h1>Monte sua pizza:</h1>
    <PizzaForm />
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import PizzaForm from "../components/PizzaForm.vue";

export default {
  name: "Home",
  components: {
    Banner,
    PizzaForm,
  },
};
</script>
