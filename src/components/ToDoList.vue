<template>
  <h1>{{ titulo1 }}</h1>

  <div class="formulario">
    <input
      v-model="tareaNueva"
      v-on:keydown.enter="agregarElemento"
      placeholder="Escribe una tarea"
    />
    <button v-on:click="agregarElemento" :disabled="deshabilitar">Agregar</button>
  </div>

  <h2>Tareas Pendientes</h2>
  <p v-if="tareasPendientes === 0">
    <span>No hay tareas por hacer</span>
  </p>
  <ul v-else>
    <li v-for="(tarea, index) in listaDeTareas" :key="index">
      {{ index }} - {{ tarea }}
      <button v-on:click="editarElemento(index, tarea)">Editar</button>
      <button v-on:click="eliminarElemento(index)">Completar</button>
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

  <hr />
  Quiero Editar la tarea: {{ index }} - {{ tareaEditar }},
  <editor-de-to-do-list
    v-if="mostrarEditor"
    v-bind:indice="index"
    v-bind:tarea="tareaEditar"
    v-on:editevent="updateToDoList"
    v-bind:tareaNueva="tareaNueva"
    />
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
      tareaEditar: '',
      index: null,

      deshabilitar: false,
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
      this.listaDeTareas.push(this.tareaNueva)
      this.tareasPendientes++
      this.tareaNueva = ''
    },
    eliminarElemento(index) {
      this.tareasCompletadas.push(this.listaDeTareas[index])
      this.listaDeTareas.splice(index, 1)
    },

    editarElemento(indice, tarea) {
      ;(this.mostrarEditor = true), (this.index = indice), (this.tareaEditar = tarea)
    },

    updateToDoList({ tarea, indice }) {
      alert('Update desde el padre, tarea:' + tarea + ' ' + indice)

      this.listaDeTareas[indice] = tarea
    },

    esaTareaEstaMuyLarga(){
      alert('ya mucho, esa tarea esta muy larga')
    }
  },

  watch: {
    tareaNueva: {
      immediate: true,
      handler() {
        if (this.tareaNueva.length === 0) {
          this.deshabilitar = true
        } else if (this.tareaNueva.length > 100) {
          this.deshabilitar = true
          this.$refs.editor.esaTareaEstaMuyLarga()
        } else {
          this.deshabilitar = false
        }
      },
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
