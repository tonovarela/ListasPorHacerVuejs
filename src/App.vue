<template>
<div id="app">
    <div class="container">

        <div class="jumbotron">
            <titulo :titulo="titulo"></titulo>
            <nueva-tarea :tareas="tareas">
            </nueva-tarea>
            <lista-tareas :tareas="tareas">
            </lista-tareas>

        </div>

    </div>
</div>
</template>

<script>
import {bus} from './main.js';
import Titulo from './Components/TituloComponent';
import NuevaTarea from './Components/NuevaTareaComponent';
import ListaTareas from './Components/ListaTareaComponent';
export default {
    name: 'app',
    components: {
        Titulo,
        NuevaTarea,
        ListaTareas
    },

    data() {
        return {

            titulo: 'Lista de Tareas',
            tareas:[],
            
        }

    },
    methods: {
        totalContador() {
            this.totalTareas = this.tareas.length;
        }
    },
    created() {
        this.$http.get("tareas.json").then(function (resultado) {
            return resultado.json();
        }).then(function (data) {
          for(let id in data){
              let tarea={
                  id:id,
                  texto:data[id].texto,
                  terminada:data[id].terminada,
              };
              this.tareas.push(tarea);
          }
           bus.actualizarContador(this.tareas.length);
        })
    }
}
</script>
