<template>
  <div class="number">
    <div class="pair" v-for="pair in pairs" :key="pair">
      <span class="title">{{pair.title}}</span>
      <span class="digits">{{pair.digits}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "DisplayNumber",
  props: {
    number: Number
  },
  computed: {
    pairs() {
      return [
        { title: "Decimal", digits: this.number },
        { title: "Binary", digits: this.number.toString(2) },
        { title: "Octal", digits: this.number.toString(8) },
        { title: "Hex", digits: this.number.toString(16) }
      ];
    }
  }
};
</script>

<style lang="scss">
.number {
  display: flex;
  flex-direction: column;
  width: 200px;
  padding: 0.2em;
  background-color: rgba(124, 188, 10, 1);
}

.pair {
  display: flex;
  flex-direction: row;
  color: black;
  line-height: 1.2em;

  background: rgb(157, 213, 58);
  background: -moz-linear-gradient(
    top,
    rgba(157, 213, 58, 1) 0%,
    rgba(161, 213, 79, 1) 50%,
    rgba(128, 194, 23, 1) 51%,
    rgba(124, 188, 10, 1) 100%
  );
  background: -webkit-linear-gradient(
    top,
    rgba(157, 213, 58, 1) 0%,
    rgba(161, 213, 79, 1) 50%,
    rgba(128, 194, 23, 1) 51%,
    rgba(124, 188, 10, 1) 100%
  );
  background: linear-gradient(
    to bottom,
    rgba(157, 213, 58, 1) 0%,
    rgba(161, 213, 79, 1) 50%,
    rgba(128, 194, 23, 1) 51%,
    rgba(124, 188, 10, 1) 100%
  );
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#9dd53a', endColorstr='#7cbc0a',GradientType=0 );

  & > * {
    width: 50%;
  }
}

.digits {
  border-left: 1px solid rgba(0, 0, 0, 0.2);
  text-align: right;
}
</style>