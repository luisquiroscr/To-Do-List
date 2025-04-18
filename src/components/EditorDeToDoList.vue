<template>
  <section>
    <h1>Editar to-do: {{ indice }} - {{ tarea }}</h1>
    <input v-model="valorActualizado"/>
    <button v-on:click="notificarPadre">Guardar</button>   <!--Cuando le da al boton se le avisa al padre y eso ocurre en methods-->
<h2>Valor Nuevo es: {{ valorActualizado }} </h2>
  {{ valorActualizado }}
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

// Mounted es una funcion de vue que sirve para indicar que el componente ya esta dentro de la pagina. Se pone por ejemplo cuando se ocupa llamar al servidor
mounted() {
  this.valorActualizado = this.tarea
},

data() {
  return {
    valorActualizado: '',
  }
},

methods: {
  notificarPadre() {
    this.$emit('editevent', {
      tarea: this.valorActualizado,
      indice: this.indice,
    })
  },
  actualiceValor(valorDelInput) {
    this.valorActualizado += valorDelInput.data
  }
}
}
</script>
