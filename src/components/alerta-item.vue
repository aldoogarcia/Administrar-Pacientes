<script setup>
import { computed} from 'vue';
        const props=defineProps({
            alert:{
                type:Object,
                required:true
            }
        })
       

        const isError= computed(()=>{
            return props.alert.tipo==='error'
            })
</script>
<template>
    <div 
    :class="[isError ? 'bg-red-600' : 'bg-green-600']"
    class=" w-full py-2 text-center text-white font-sans">
        <strong>{{ alert.mensaje }} </strong>
    </div>
</template>


