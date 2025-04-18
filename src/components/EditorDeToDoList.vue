<template>
  <section>
    <h1>Editar to-do: {{ indice }} - {{ tarea }}</h1>
    <input v-bind:value="tarea"/>
    <button v-on:click="notificarPadre">Guardar</button>   <!--Cuando le da al boton se le avisa al padre y eso ocurre en methods-->
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
},

methods: {
  notificarPadre() {
    this.$emit('editevent')
  }
}
}
</script>
