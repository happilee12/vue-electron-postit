<template>
  <v-row>
    <v-col md="6" pa-10>
      <PieChart chartId="1" :chartData="pieChartData.category" />
    </v-col>
    <v-col md="6">
      <PieChart chartId="2" :chartData="pieChartData.subcategory" />
    </v-col>
  </v-row>
</template>

<script>
import PieChart from "@/components/VueChart/PieChart.vue";
import { getCategoryRatioDataset } from "@/js/categoryStstisticsChart";
export default {
  name: "CategoryPieChart",
  components: { PieChart },
  props: {
    memoItems: {
      type: Array,
    },
    dateRange: {
      type: Array,
      default: [],
    },
  },
  computed: {
    pieChartData: function () {
      try {
        const { category, subcategory } = getCategoryRatioDataset(
          this.memoItems
        );
        return {
          category,
          subcategory,
        };
      } catch (e) {
        console.log(e);
        return {
          labels: [],
          datasets: [],
        };
      }
    },
  },
};
</script>

<style lang="scss"></style>
