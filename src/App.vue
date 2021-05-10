<template>
  <div>
    <Card>
      <Header title="Tabuada challenge" />
    </Card>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header";
import Card from "./components/Card";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Footer,
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
body{
  background-color: rgb(151 151 151 / 10%);
}
</style>
