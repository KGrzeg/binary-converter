<template>
  <div class="insert">
    <input type="text" v-model="raw_number" />
    <select v-model="format">
      <option value="dec">Decimal</option>
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
      alert(this.raw_number);
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
