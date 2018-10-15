<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-primary">
      <a href="/" class="navbar-brand">Conexion Firebase y vuejs</a>
    </nav>
    <div class="container">
      <div class="row mt-5 ">
        <div class="col-md-4">
          <div class="card-header">
            <h3> Agrega al alumno</h3>
          </div>
          <div class="card-body">
            <form @submit.prevent="btnGuardar">
              <div class="form-group">
                  <input type="text" placeholder="Nombre" v-model="datoAlumno.name" class="form-control"/>
              </div>
              <div class="form-group">
                  <input type="text" placeholder="Materia" v-model="datoAlumno.materia" class="form-control"/>
              </div>
              <div class="form-group">
                  <input type="text" placeholder="Nota" v-model="datoAlumno.nota" class="form-control"/>
              </div>
              <div class="form-group">
                  <input type="text" placeholder="Profesor" v-model="datoAlumno.profesor" class="form-control"/>
              </div>
              <button class="btn btn-primary" type="submit">
                Guardar
              </button>
            </form>
          </div>
        </div>
        <div class="col-md-8">
          <div class="card">
            <div class="card-header">
              <h3>Alumnos</h3>
            </div>
            <div class="card-body">
              <table class="table table-striped table-bordered" >
                <thead>
                    <tr>
                      <th>Nombre</th>
                      <th>Materia</th>
                      <th>Nota</th>
                      <th>Profersor</th>
                      <th>Accion</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="dato in bdAlumnos">
                      <td>{{dato.name}}</td>
                      <td>{{dato.materia}}</td>
                      <td>{{dato.nota}}</td>
                      <td>{{dato.profesor}}</td>
                      <td>
                        <button class="btn btn-primary" @click="delAlum(dato)">Editar</button>
                        <button class="btn btn-danger" @click="ediAlum(dato)">Eliminar</button> </td>

                    </tr>
                </tbody>
              </table>
            </div>
          </div>
          <br/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  //importaciones
import Firebase from 'firebase';
import config from './config';
import toastr from 'toastr';

let app = Firebase.initializeApp(config);
let db = app.database();
let refAlum = db.ref('bdAlumnos')

export default {
  name: 'App',
  firebase: {
    bdAlumnos: refAlum
  },
  data () {
    return{
       datoAlumno: {
         name: '',
         materia: '',
         nota: '',
         profesor: ''
       }
    }
  },
  methods: {
    btnGuardar() {
      refAlum.push(this.datoAlumno);
      toastr.success('Datos guardados correctamente');
      this.datoAlumno.profesor='';
      this.datoAlumno.nota='';
      this.datoAlumno.materia='';
      this.datoAlumno.name='';
    },
    delAlum(alumno) {
      refAlum.child(alumno['.key']).remove();
      toastr.success('Datos eliminados correctamente')
    },
    ediAlum(alumno) {
      refAlum.child(alumno['.key']).update(this.datoAlumno);
      toastr.success('Datos eliminados correctamente')
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
  margin-top: 10px;

}
</style>
