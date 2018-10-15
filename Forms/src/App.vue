<template>
  <div id="app">
    <div class="container">
      <div class="row">
          <div class="col-md-11">
            <div  class="card mb-3">
              <div class="card-body">
                  <h4 class="card-title"> agregar Palabras </h4>
                  <div class="est_form" v-on:submit.prevent="actEstu">
                      <input type="text" class="form-control mb-2" placeholder="Palabra 1"
                             v-model="actEstu.name" />
                      <input type="text" class="form-control mb-2" placeholder="Palabra 2"
                             v-model="actEstu.materia"  />
                      <input type="text" class="form-control mb-2" placeholder="Palabra 3"
                             v-model="actEstu.nota"   />
                    <input type="text" class="form-control mb-2" placeholder="Palabra 4"
                             v-model="actEstu.profe"   />
              </div>
            </div>
          </div>
          </div>
          <div class="col-md-1">

      <button class="button btn btn mt-5 mb-5" style="background-color:#0cccff;"
        @click.prevent="newEst">
          Only words in this order
      </button>
        <div class="card-1">
          <p style="text-align: center">
            <a>1  hola </a>
             <a> 2amarillo</a>
              <a>3 libro</a>
                <a>4leon</a>
          </p>
        </div>
          </div>
      </div>
      <hr>
      <div class="card">
        <div class="card-header">
          <h3>Palabras</h3>
        </div>
        <div class="card-body">
          <table class="table table-striped" >
            <thead>
              <tr>
                <th>Traduccion 1 </th>
                <th >Traduccion 2</th>
                <th>Traduccion 3</th>
                <th>Traduccion 4</th>
              </tr>
            </thead>
            <tbody>
                <tr>
                    <td>
                      <a v-if="actEstu.name=='hola'"> {{actEstu.name}} = Hello! </a>
                    </td>
                    <td>
                      <a v-if="actEstu.materia=='amarillo'" >{{actEstu.materia}} = Yellow </a>
                    </td>
                     <td >
                     <a v-if="actEstu.nota=='libro'"> {{actEstu.nota}} = Book </a>
                    </td>
                     <td>
                      <a v-if="actEstu.profe=='leon'" > {{actEstu.profe}} = Lion</a>
                    </td>
                </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  data() {
    return {
      actEstu:{
        name: '',
        materia: '',
        nota: '',
        profe: ''
      }
    }
  },
  methods: {
    newEst (){
      console.log(this.actEstu.name);
    },
    deleteEst (index) {
      this.newEst.splice(index,1);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
