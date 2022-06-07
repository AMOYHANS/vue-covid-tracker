<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- box1 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">病例</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">新增:</span>
        {{ numberWithCommas(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">总数:</span>
        {{ numberWithCommas(stats.TotalConfirmed) }}
      </div>
    </div>
    <!-- box2 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">死亡</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">新增:</span>
        {{ numberWithCommas(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">总数:</span>
        {{ numberWithCommas(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  methods: {
    numberWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>