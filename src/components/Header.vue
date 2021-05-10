<template>
  <div>
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
  },
};
</script>

<style scoped>
div {
  margin-bottom: 15px;
  text-align: center;
}
h1 {
  color: rgba(0, 0, 0, 0.7);
}
</style>
