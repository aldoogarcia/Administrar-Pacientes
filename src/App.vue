<script setup>
import {ref,reactive, onMounted, watch} from 'vue'
import {uid}from 'uid'
import headerItem from './components/header-item.vue';
import formularioItem from './components/fromulario-item.vue';
import personaItem from './components/persona-item.vue';
const muestra=ref(true)


const paciente = reactive({
                id:null,
                nombre: '',
                propietario: '',
                email: '',
                alta: '',
                sintomas: ''
            })
const pacientes= ref([])

const guardarPaciente = () => {
  if (paciente.id){
    // tambien su pudo a ver destructurizado
    // const {id} paciente
    const i =pacientes.value.findIndex(pacienteStok => pacienteStok.id == paciente.id);
    pacientes.value[i]={...paciente}
  }else{
    pacientes.value.push({
    ...paciente,
    id: uid()
  })
  }




  paciente.nombre = ''
  paciente.propietario = ''
  paciente.email = ''
  paciente.alta=''
  paciente.sintomas=''
  paciente.id=null
  }

const ActualizarPaciente=(id)=>{
  const pacienteEditar = pacientes.value.find(paciente => paciente.id === id);
  Object.assign(paciente, pacienteEditar);
 
}

const eliminarPaciente=(id)=>{
 pacientes.value= pacientes.value.filter(pacienteE => pacienteE.id !== id)
 
}
onMounted(()=>{
  const pacienteStorage= localStorage.getItem("pacientes")
if(pacienteStorage){
  pacientes.value=JSON.parse(pacienteStorage)
  console.log(pacientes.value)
}
}
)

watch(pacientes,()=>{
  guardarLocalStorage()
},
{deep:true}
)

const guardarLocalStorage=()=>{
  localStorage.setItem("pacientes",JSON.stringify(pacientes.value))
}

</script>

<template>
  <div class="container mx-auto mt-20">
    <headerItem
    v-if="muestra"
    />
    <div class="md:flex">
      <formularioItem
      v-model:nombre="paciente.nombre"
      v-model:propietario="paciente.propietario"
      v-model:email="paciente.email"
      v-model:alta="paciente.alta"
      v-model:sintomas="paciente.sintomas"
      v-model:id="paciente.id"
      @agregar-persona="guardarPaciente"
      


      />
      <div class="md:w-1/2 text-xl text-center mt-5 " >

        <h3 class="text-3xl">Administrar a tus paciente</h3>
        <p class="text-lg text-center mb-10">Añade ¨Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>
        <div v-if="pacientes.length>0">
          <personaItem
            v-for="paciente in pacientes"
            :paciente="paciente"
            @actualizar-paciente="ActualizarPaciente"
            @eliminar-paciente="eliminarPaciente"
            class="text-left"
          />
          
        </div>
        <div v-else>
          <p class="text-center  mt-20">No hay citas</p>
        </div>
    </div>

    </div>
  </div>
</template>

