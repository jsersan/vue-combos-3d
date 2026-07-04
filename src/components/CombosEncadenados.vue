<template>
    <div class="min-h-screen bg-gray-100 flex items-center justify-center p-4">
      <div class="bg-white rounded-lg shadow-md p-6 w-full max-w-md">
        <h1 class="text-2xl font-bold mb-6 text-center text-gray-800">Selección de Ubicación</h1>
        
        <div class="space-y-4">
          <div>
            <label for="pais" class="block text-sm font-medium text-gray-700 mb-1">País</label>
            <select
              id="pais"
              v-model="paisSeleccionado"
              @change="cargarEstados"
              class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md"
            >
              <option value="">Selecciona un país</option>
              <option v-for="pais in paises" :key="pais.id" :value="pais.id">{{ pais.nombre }}</option>
            </select>
          </div>
  
          <div>
            <label for="estado" class="block text-sm font-medium text-gray-700 mb-1">Estado/Provincia</label>
            <select
              id="estado"
              v-model="estadoSeleccionado"
              @change="cargarCiudades"
              :disabled="!paisSeleccionado"
              class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md"
            >
              <option value="">Selecciona un estado/provincia</option>
              <option v-for="estado in estados" :key="estado.id" :value="estado.id">{{ estado.nombre }}</option>
            </select>
          </div>
  
          <div>
            <label for="ciudad" class="block text-sm font-medium text-gray-700 mb-1">Ciudad</label>
            <select
              id="ciudad"
              v-model="ciudadSeleccionada"
              :disabled="!estadoSeleccionado"
              class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md"
            >
              <option value="">Selecciona una ciudad</option>
              <option v-for="ciudad in ciudades" :key="ciudad.id" :value="ciudad.id">{{ ciudad.nombre }}</option>
            </select>
          </div>
        </div>
  
        <div v-if="seleccionCompleta" class="mt-6 p-4 bg-green-100 rounded-md">
          <p class="text-green-700">Has seleccionado:</p>
          <p class="font-semibold">{{ seleccionTexto }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  
  // Datos simulados (en una aplicación real, estos vendrían de una API de Node.js)
  const paises = [
    { id: 1, nombre: 'España' },
    { id: 2, nombre: 'Francia' },
    { id: 3, nombre: 'Italia' }
  ]
  
  const estadosPorPais = {
    1: [
      { id: 1, nombre: 'Euskadi' },
      { id: 2, nombre: 'Navarra' },
      { id: 3, nombre: 'Canarias' }
    ],
    2: [
      { id: 4, nombre: 'Ìle de France' },
      { id: 5, nombre: 'Nueva Aquitania' },
      { id: 6, nombre: 'Ocitania' }
    ],
    3: [
      { id: 7, nombre: 'Lazzio' },
      { id: 8, nombre: 'Toscana' },
      { id: 9, nombre: 'Veneto' }
    ]
  }

  
  const ciudadesPorEstado = {
    1: [{ id: 1, nombre: 'Vitoria' }, { id: 2, nombre: 'Donostia' }, { id: 3, nombre: 'Bilbao' }],
    2: [{ id: 4, nombre: 'Iruña' }, { id: 5, nombre: 'Estella' }, { id: 6, nombre: 'Tudela' }],
    3: [{ id: 7, nombre: 'Las Palmas' }, { id: 8, nombre: 'Agaete' }, { id: 9, nombre: 'Arrecife' }],
    4: [{ id: 10, nombre: 'París' }, { id: 11, nombre: 'Sant-Dennis' }, { id: 12, nombre: 'Versailles' }],
    5: [{ id: 13, nombre: 'Burdeos' }, { id: 14, nombre: 'Biarritz' }, { id: 15, nombre: 'Limoges' }],
    6: [{ id: 16, nombre: 'Tolouse' }, { id: 17, nombre: 'Montpelier' },{ id: 18, nombre: 'Perpiñán' }],
    7: [{ id: 19, nombre: 'Roma' }, { id: 20, nombre: 'Frosinone' },{ id: 21, nombre: 'Rieti' }],
    8: [{ id: 22, nombre: 'Florencia' }, { id: 23, nombre: 'Pisa' },{ id: 24, nombre: 'Siena' }],
    9: [{ id: 25, nombre: 'Venezia' }, { id: 26, nombre: 'Trevisso' }, { id: 27, nombre: 'Padua' }]
  }
  
  const paisSeleccionado = ref('')
  const estadoSeleccionado = ref('')
  const ciudadSeleccionada = ref('')
  
  const estados = ref([])
  const ciudades = ref([])
  
  const cargarEstados = () => {
    estados.value = estadosPorPais[paisSeleccionado.value] || []
    estadoSeleccionado.value = ''
    ciudadSeleccionada.value = ''
    ciudades.value = []
  }
  
  const cargarCiudades = () => {
    ciudades.value = ciudadesPorEstado[estadoSeleccionado.value] || []
    ciudadSeleccionada.value = ''
  }
  
  const seleccionCompleta = computed(() => 
    paisSeleccionado.value && estadoSeleccionado.value && ciudadSeleccionada.value
  )
  
  const seleccionTexto = computed(() => {
    if (seleccionCompleta.value) {
      const pais = paises.find(p => p.id === parseInt(paisSeleccionado.value))
      const estado = estados.value.find(e => e.id === parseInt(estadoSeleccionado.value))
      const ciudad = ciudades.value.find(c => c.id === parseInt(ciudadSeleccionada.value))
      return `${ciudad.nombre}, ${estado.nombre}, ${pais.nombre}`
    }
    return ''
  })
  </script>