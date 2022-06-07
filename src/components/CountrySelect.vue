<template>
  <select
    @change="onChange()"
    v-model="selected"
    class="form-select mt-10 block w-full border p-2 rounded-xl bg-gray-100"
  >
    <option value="0">选择国家</option>
    <option :value="c.ID" v-for="c in countries" :key="c">
      {{ c.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => this.selected === item.ID);
      this.$emit("get-country", country);
    },
  },
};
</script>
