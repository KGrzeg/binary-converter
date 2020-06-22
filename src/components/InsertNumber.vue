<template>
  <div class="insert">
    <input type="text" v-model="raw_number" />
    <select v-model="format">
      <option value="dec">Decimal</option>
      <option value="bin">Binary</option>
      <option value="oct">Octal</option>
      <option value="hex">Hex</option>
      <option value="u2">Binary U2</option>
      <option value="zm">Binary ZM</option>
      <option value="ieee">Binary IEEE-754 32bits</option>
      <option value="bcd">BCD</option>
    </select>
    <button @click="submit">Update</button>
  </div>
</template>

<script>
const showError = msg => alert(msg || "Error");
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

      if (isNaN(number)) {
        showError();
      } else {
        this.$emit("newnumber", number);
      }
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
    },
    u2() {
      const re = /^[01]+$/;
      if (!re.test(this.raw_number)) {
        showError("Invalid format");
        return 0;
      }

      let number = 0;
      let pow = 0;

      for (let i = this.raw_number.length - 1; i >= 0; i--) {
        const digit = this.raw_number[i];

        if (digit === "1") {
          const mul = i == 0 ? -1 : 1;
          number += 2 ** pow * mul;
        }

        ++pow;
      }
      return number;
    },
    zm() {
      const sign = this.raw_number[0] === "1" ? -1 : 1;
      const num = parseInt(this.raw_number.substring(1), 2);
      return sign * num;
    },
    ieee() {
      const sign = this.raw_number[0] === "1" ? -1 : 1;
      const e = parseInt(this.raw_number.substring(1, 9), 2);
      const m = parseInt(this.raw_number.substring(9), 2);

      return sign * (1 + m / 2 ** 23) * 2 ** (e - 127);
    },
    bcd() {
      if (this.raw_number.length % 4 !== 0) {
        showError("Invalid format");
        return 0;
      }
      let number = 0;

      for (let i = 0; i < this.raw_number.length; i += 4) {
        const chunk_raw = this.raw_number.substring(i, i + 4);
        const chunk = parseInt(chunk_raw, 2);

        if (chunk > 9) {
          showError("Invalid format");
          return 0;
        }

        number *= 10;
        number += chunk;
      }

      return number;
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
