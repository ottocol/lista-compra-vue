<template>
  <div>
   <label>Nombre:</label> <input type="text" v-model="nombre" placeholder="Nombre..."/> <br>
   <label>Cantidad:</label> <input type="number" v-model="cantidad" placeholder="Nombre..."/> <br>
   <label>Comentarios</label><br>
   <textarea v-model="comentario" placeholder="Comentario sobre el item..."></textarea> <br>
   <button @click="addItem">Añadir</button>
  </div>    
</template>


<script>
export default {
   name: 'NuevoItem',
   data: function() {
       return {
         nombre:"",
         cantidad: 0,
         comentario:""
       }
   },
   methods: {
       addItem: function() {
          this.$emit('nuevo', {nombre:this.nombre, cantidad:this.cantidad, comentario:this.comentario})
       }
   } 
}
</script>


<style scoped>

</style>