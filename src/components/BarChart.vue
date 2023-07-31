<script setup>
import { computed, ref } from "vue";
const props = defineProps({
  stats: Array,
  name:String
});
const options = {
  chart: {
    id: "vuechart-example",
  },
  xaxis: {
    categories: [
      "PV" + props.name,
      "Ataque",
      "Defensa",
      "Ataque ES",
      "Defensa ES",
      "Velocidad",
    ],
  },
};

const apexChart = ref(null)


const series = computed(() => {
  return [
    {
      name: "Estadistica",
      data: props.stats,
    },
  ];
});
</script>
<template>
  <div>
    <apexchart
      ref="apexChart"
      width="500"
      type="bar"
      :options="options"
      :series="series"
      :key="props.name"
    ></apexchart>
   
  </div>
</template>