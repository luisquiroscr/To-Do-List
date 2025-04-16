<template>
  <section>
    <h1>Editar to-do: {{ index }} - {{ tarea }}</h1>
    <input v-bind:value="tarea"/>
    <button>Guardar</button>
  </section>
</template>


<script>
export default {
  props: {
    tarea: {
      type: String,
  },

  indice: {
    type: Number,
}
}
}
</script>
