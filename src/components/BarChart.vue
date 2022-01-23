<script setup>
import {computed} from 'vue'
const props = defineProps({
    stats:Array
})
const options = {
        chart: {
          id: 'vuechart-example'
        },
        xaxis: {
          categories: ['PV', 'Ataque', 'Defensa', 'Ataque ES', 'Defensa ES', 'Velocidad']
        }
      }
const series = computed(()=>{
    return [
        {
            name:'Estadistica',
            data:props.stats
        }
    ]
})
</script>
<template>
    <div>
        <apexchart width="500" type="bar" :options="options" :series="series"></apexchart>
    </div>
</template>