<template>
  <div id="app">
    <InsertNumber @newnumber="updateNumber" />
    <DisplayNumber :number="number" />
  </div>
</template>

<script>
import DisplayNumber from "@/components/DisplayNumber.vue";
import InsertNumber from "@/components/InsertNumber.vue";

export default {
  name: "App",
  data() {
    return {
      number: 0
    };
  },
  components: { DisplayNumber, InsertNumber },
  methods: {
    updateNumber(number) {
      this.number = number;
    }
  }
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
