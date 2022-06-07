<template>
  <main class="" v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelect :countries="countries" @get-country="getCountry" />
    <button
      v-if="stats.Country"
      @click="clearCountryData"
      class="
        mt-10
        bg-green-700
        text-white
        rounded
        p-2
        focus:outline-none
        hover:bg-green-600 hover:text-gray-600
      "
    >
      查看全球
    </button>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 trext-3xl mt-10 mb-6">加载数据中...</div>
    <img :src="loadingImage" alt="Logo" class="w-24 m-auto" />
  </main>
</template>

<script>
import DataTitle from "../components/DataTitle.vue";
import DataBoxes from "../components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
  name: "HomeView",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "全球",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountry(c) {
      this.stats = c;
      this.title = c.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.stats = data.Global;
      this.title = "全球";
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.loading = false;
    this.countries = data.Countries;
  },
};
</script>
