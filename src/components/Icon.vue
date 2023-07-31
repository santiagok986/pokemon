<script setup>
import {toRefs} from 'vue';

const props = defineProps({
   iconPath:{
     type:String, 
     required:true
   },
   size:{type:String, default:"32"},
   viewBox: {type:String, default:"0 0 24 24"},
})

const {size, viewBox, iconPath,} = toRefs(props)

</script>

<template>
    <svg :width="size" :height="size" :viewBox="viewBox" color="currentColor" fill='currentColor'>
        <path :d="iconPath"></path>
    </svg>
</template>