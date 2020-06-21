<template>
  <div class="insert">
    <input type="text" v-model="raw_number" />
    <select v-model="format">
      <option value="dec">Decimal</option>
      <option value="bin">Binary</option>
      <option value="oct">Octal</option>
      <option value="hex">Hex</option>
    </select>
    <button @click="submit">Zapisz</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      raw_number: 0,
      format: "dec"
    };
  },
  methods: {
    submit() {
      const transformFunction = this[this.format];

      const number = transformFunction(this.raw_number);

      this.$emit("newnumber", number);
    },
    dec() {
      return parseFloat(this.raw_number);
    },
    bin() {
      return parseInt(this.raw_number, 2);
    },
    oct() {
      return parseInt(this.raw_number, 8);
    },
    hex() {
      return parseInt(this.raw_number, 16);
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/variables.scss";

.insert {
  display: flex;
  flex-direction: column;
  width: $widget-width;
  padding: 0.2em;
  background-color: rgba(124, 188, 10, 1);
}
</style>
