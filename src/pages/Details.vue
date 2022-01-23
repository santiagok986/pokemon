<script setup>
import { useRoute } from "vue-router";
import BarChart from "../components/BarChart.vue";
import RadarChart from "../components/RadarChart.vue";
import { reactive, toRefs, computed, ref, onMounted, watch } from "vue";
const state = reactive({
  pokemon: null,
  stats: computed(() => filterStats()),
  types: computed(() => filterTypes()),
});

function filterStats() {
  if (state.pokemon) {
    return state.pokemon.stats.map((stat) => stat.base_stat);
  }
}

function filterTypes() {
  if (state.pokemon) {
    return state.pokemon.types.map((type) => type.type.name);
  }
}

const route = useRoute();
const { pokemon, stats, types } = toRefs(state);

const getData = async () => {
  await fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.id}`)
    .then((res) => res.json())
    .then((data) => {
      state.pokemon = data;
    });
};

watch(route,()=>{
    getData()
})

onMounted(()=>{
    getData()
})

///cambio de grafica
const isBarChart = ref(true);

const changeChart = () => {
  isBarChart.value = !isBarChart.value;
};

//console.log(route.params.id)
</script>
<template>
  <div>
    <div v-if="pokemon">
      <div class="w-4/6 mx-auto rounded-xl p-10 shadow-lg">
        <h1 class="font-black md:text-3xl text-xl text-red-900 mb-2">
          {{ pokemon.name }}
        </h1>
        <span
          v-for="type in types"
          :key="type"
          class="
            py-1
            px-2
            shadow-md
            rounded-full
            bg-red-500
            text-white
            font-semibold
            mr-2
            mt-3
          "
        >
          {{ type }}
        </span>

        <div class="flex flex-wrap">
          <div class="flex-1 grid place-items-center">
            <img
              class="w-48 h-48"
              :src="pokemon.sprites.front_default"
              :alt="`imagen de ${pokemon.name}`"
            />
          </div>
          <div class="flex-1">
            <button @click="changeChart()">
              {{ isBarChart ? "Radar" : "Bar" }}
            </button>
            <!-- <bar-chart :stats="stats"/> -->
            <component
              :is="isBarChart ? BarChart : RadarChart"
              :stats="stats"
            />
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <p>No hay datos disponibles</p>
    </div>
  </div>
</template>