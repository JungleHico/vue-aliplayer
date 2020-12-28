<template>
  <div id="app">
    <example></example>
  </div>
</template>

<script>
import Example from "./views/Example";

export default {
  name: "App",
  components: {
    Example
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
