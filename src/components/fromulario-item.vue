        <script setup>
import { reactive } from 'vue';
import alertaItem from './alerta-item.vue'

            const alerta=reactive({
                mostrar:false,
                mensaje:'',
                muestraItem:false,
            })

            const props=defineProps({
                nombre:{
                    type:String,
                    required:true
                },
                propietario:{
                    type:String,
                    required:true
                },
                email:{
                    type:String,
                    required:true
                },
                alta:{
                    type:String,
                    required:true
                },
                sintomas:{
                    type:String,
                    required:true
                }
            })
            const validar=()=>{
                const llenos =Object.values(props).includes('');
                if(llenos){
                    alerta.mostrar=true;
                    alerta.muestraItem=true;
                    alerta.mensaje='Todos los campos son obligatorios';
                    return
                }else{
                    alerta.mostrar=false;
                    alerta.muestraItem=true;
                    alerta.mensaje='Se ha guardado correctamente';
                    emit('agregar-persona')
                    return
                }
            }
            const emit=defineEmits(['update:nombre', 'update:propietario','update:email', 'update:alta','update:sintomas','agregar-persona'])
        </script>
<template>
    <div class="md:w-1/2 mt-5">¬
        <h2 class="font-serif text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg text-center mb-10">Añade ¨Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>

<alertaItem
v-if="alerta.muestraItem"
:alert="alerta"
/>

        <form @submit.prevent="validar"
        class="bg-white shadow-xl rounded-xl py-10 px-5 mb-10 font-sans ">
            <div class="mb-5">
                <label for="mascota" class="text-gray-950 uppercase font-sans">Nombre Mascota</label>
                <input id="mascota" type="text" placeholder="Nombre de la mascota" @input="$emit('update:nombre',$event.target.value)"
                 class="block mt-3  border-2 w-full p-1 rounded-3xl shadow-md">
            </div>
            <div class="mb-5">
                <label for="propietario" class="text-gray-950 uppercase ">Nombre propietario</label>
                <input id="propietario" type="text" placeholder="Nombre del propietario"  @input="$emit('update:propietario',$event.target.value)"
                 class="block mt-3  border-2 w-full p-1 rounded-3xl shadow-md mb-3">
            </div>
            <div class="mb-5">
                <label for="email" class="text-gray-950 uppercase ">Email</label>
                <input id="email" type="email" placeholder="aldo@correo.com"  @input="$emit('update:email',$event.target.value)"
                 class="block mt-3  border-2 w-full p-1 rounded-3xl shadow-md mb-3">
            </div>
            <div class="mb-5">
                <label for="alta" class="text-gray-950 uppercase ">Alta</label>
                <input id="alta" type="date" placeholder="Nombre de la mascota" @input="$emit('update:alta',$event.target.value)"
                 class="block mt-3  border-2 w-full p-1 rounded-3xl shadow-md mb-3">
            </div>
            <div class="mb-5">
                <label for="sintomas" class="text-gray-950 uppercase ">sintomas</label>
                <textarea  id="sintomas" placeholder="Describe los sintomas"  v @input="$emit('update:sintomas',$event.target.value)"
                class="h-20 border-l-purple-500 w-full shadow-xl placeholder-gray-500 mb-3 rounded-md uppercase">

                </textarea>
            </div>
            <input  type="submit" value="Enviar" class="w-full bg-blue-600 text-white py-2 hover:bg-blue-700
                transition-colors">
        </form>
    </div>

    
</template>
