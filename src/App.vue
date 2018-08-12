<template>
<div id="app">
    <div class="container">

        <div class="jumbotron">
            <titulo :titulo="titulo" ></titulo>
            <nueva-tarea :tareas="tareas" >
            </nueva-tarea>
            <lista-tareas :tareas="tareas" >
            </lista-tareas>

        </div>

    </div>
</div>
</template>

<script>
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
            tareas: [{
                    texto: "Aprender VUE.js",
                    terminar: false
                }, {
                    texto: "Aprender Angula2",
                    terminar: false
                },
                {
                    texto: "Aprender Ionic 2",
                    terminar: false
                }
            ],
           
            
        }

    },
    methods: {
        totalContador() {
            this.totalTareas = this.tareas.length;
        }
    }
}
</script>
