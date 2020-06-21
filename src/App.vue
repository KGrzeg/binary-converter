<template>
  <div id="app">
    <DisplayNumber :number="200" />
  </div>
</template>

<script>
import DisplayNumber from "@/components/DisplayNumber.vue";

export default {
  name: "App",
  components: { DisplayNumber }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

body {
  background-color: #111;
  color: yellowgreen;
  font-family: "Lucida Console", "Courier New", Courier, monospace;
}
</style>
