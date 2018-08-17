<template>
<ul class="list-group">
    <li class="list-group-item" v-for="(tarea,indice) of tareas" :key="tarea.id" v-bind:class="{terminada:tarea.terminada}">
        {{tarea.texto}} 
        <span class="pull-right">
            <button class="btn btn-success btn-xs glyphicon glyphicon-ok" @click="estado(indice)">
            </button>
            <button class="btn btn-danger btn-xs glyphicon glyphicon-remove" @click="borrar(indice)" ></button>
        </span>

    </li>
</ul>
</template>

<script>
import {
    bus
} from './../main.js';
export default {
    props: ['tareas'],
    data() {
        return {}
    },
    methods: {
        borrar: function (indice) { 
            
             let id = this.tareas[indice].id;
             this.tareas.splice(indice, 1);
            this.$http.delete("tareas/"+id+".json").then(respuesta=>{console.log(respuesta)});
            bus.actualizarContador(this.tareas.length);

        },
        estado(indice) {
            let terminada = this.tareas[indice].terminada = !this.tareas[indice].terminada;
            let id = this.tareas[indice].id;

            this.$http.patch('tareas/' + id + ".json", {
                terminada: terminada
            }).then(respuesta=>console.log(respuesta));
        }

    }
}
</script>

<style scoped>
.terminada {
    color: gray;
    text-decoration: line-through;
}
</style>
