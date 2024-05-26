<script setup>
import { computed } from 'vue';
        const props=defineProps({
            alert:{
                type:Object,
                required:true
            }
        })

        const isError= computed(()=>{
            return props.alert.muestraItem===false
            })
</script>
<template>
    <div 
    :class="[isError ? 'bg-green-600' : 'bg-red-600']"
    class=" w-full py-2 text-center text-white font-sans">
        <strong>{{ alert.mensaje }}  {{ alert.muestra }}</strong>
    </div>
</template>


