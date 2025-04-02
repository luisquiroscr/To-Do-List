<template>
  <h1>{{ titulo1 }}</h1>

  <div class="formulario">
    <input v-model="tareaNueva" placeholder="Escribe una tarea" />
    <button v-on:click="agregarElemento">Agregar</button>
  </div>

  <h2>Tareas Pendientes</h2>
  <p v-if="tareasPendientes === 0">
    <span>No hay tareas por hacer</span>
  </p>
  <ul v-else>
    <li v-for="(tarea, index) in listaDeTareas" :key="index">
      {{ index }} - {{ tarea }}
      <button v-on:click="editarElemento">Editar</button>
      <button v-on:click="eliminarElemento(index)">Eliminar</button>
    </li>
  </ul>

  <h2>Tareas Completadas</h2>
  <p v-if="contadorDeTareasCompletadas === 0">
    <span>No hay tareas completadas</span>
  </p>
  <ul v-else style="min-height: 100px; background-color: green">
    <li v-for="(tarea, index) in tareasCompletadas" :key="index">{{ index }} - {{ tarea }}</li>
  </ul>

  <h2>Resumen de tareas</h2>
  <p>Completadas: {{ contadorDeTareasCompletadas }} | Pendientes: {{ tareasPendientes }}</p>
  <p>Total de tareas: {{ totalDeTareas }}</p>


<hr/>
<editor-de-to-do-list v-if="mostrarEditor"/>



</template>

<script>

import EditorDeToDoList from './EditorDeToDoList.vue'

export default {
  data() {
    return {
      titulo1: 'Aprendizaje de Vue',
      listaDeTareas: [],
      tareaNueva: '',
      tareasCompletadas: [],

      mostrarEditor: false,
    }
  },

  computed: {
    tareasPendientes() {
      return this.listaDeTareas.length
    },
    contadorDeTareasCompletadas() {
      return this.tareasCompletadas.length
    },
    totalDeTareas() {
      return this.listaDeTareas.length + this.tareasCompletadas.length
    },
  },

  methods: {
    agregarElemento() {
      if (this.tareaNueva.trim() !== '') {
        this.listaDeTareas.push(this.tareaNueva.trim())
        this.tareaNueva = ''
      }
    },
    eliminarElemento(index) {
      this.tareasCompletadas.push(this.listaDeTareas[index])
      this.listaDeTareas.splice(index, 1)
    },

    editarElemento() {
      alert ('editar')
    },


  },

  components: {
    'editor-de-to-do-list': EditorDeToDoList,
  },
}
</script>

<style scoped>
.formulario {
  display: block;
  background-color: red;
}
</style>
