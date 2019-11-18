<template>
  <div id="app">
    <h1>Lista de la compra</h1>
    <nuevo-item @nuevo="addItem"/>
    <lista :items="items"/>
  </div>
</template>

<script>
import Lista from './components/Lista.vue'
import NuevoItem from './components/NuevoItem.vue'
import Servicio_API from './services/API_lista'

export default {
  name: 'app',
  components: {
    Lista,
    NuevoItem
  },
  data: function() {
    return { 
        items : [],
        api : new Servicio_API('http://localhost:3000/api/items')
    }
  },
  //Función del ciclo de vida de Vue. Cuando el componente se "monta",
  //o sea se pinta por primera vez en la página. Cada repintado ya no llama a esto
  beforeMount: function() {
    this.api.obtenerItems()
      //IMPORTANTE: se usa una función de flecha (=>) para que "this" signifique lo mismo
      //que en el contexto de la función: el componente Vue. si usáramos function()
      //this sería el objeto global 'window', al ser esto un callback llamado por el navegador
      .then((lista)=>{
        //Añado los elementos uno por uno porque usando concat no se disparaba la reactividad de Vue
        lista.forEach((dato)=>{
          this.items.push(dato)
        })
      })
  },
  methods: {
    addItem: function(datos) {
       //this.items.push({id:this.idActual, nombre:e})
       //this.idActual++
       this.api.addItem(datos)
        //IMPORTANTE: se usa una función de flecha (=>) por la misma razón que más arriba
        .then((datosResp)=>{
          window.console.log(datosResp)
          this.items.push(datosResp)
        })       
    }
  } 
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
