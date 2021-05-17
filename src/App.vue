<template>
  <div>
    <Card>
      <Header title="Tabuada challenge" />
    </Card>
  </div>
</template>

<script>
import Header from "./components/Header";
import Card from "./components/Card";

export default {
  name: "App",
  components: {
    Card,
    Header,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;400;500;700;800&display=swap");
html {
  font-family: "Montserrat", sans-serif;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
