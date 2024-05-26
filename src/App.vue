<script setup>
import {ref,reactive} from 'vue'
import headerItem from './components/header-item.vue';
import formularioItem from './components/fromulario-item.vue';
import personaItem from './components/persona-item.vue';
const paciente = reactive({
                nombre: '',
                propietario: '',
                email: '',
                alta: '',
                sintomas: ''
            })
const pacientes= ref([])

const guardarPaciente = () => {
  pacientes.value.push(paciente)
  }
</script>

<template>
  <div class="container mx-auto mt-20">
    <headerItem/>
    <div class="md:flex">
      
      <formularioItem
      v-model:nombre="paciente.nombre"
      v-model:propietario="paciente.propietario"
      v-model:email="paciente.email"
      v-model:alta="paciente.alta"
      v-model:sintomas="paciente.sintomas"
      @agregar-persona="guardarPaciente"

      />
      <div class="md:w-1/2 text-xl text-center mt-5 " >

        <h3 class="text-3xl">Administrar a tus paciente</h3>
        <p class="text-lg text-center mb-10">Añade ¨Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>
        <div v-if="pacientes.length>0">
          <personaItem
            v-for="pacciente in pacientes"
            :paciente="pacciente"
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

